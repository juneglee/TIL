# Embedding

## 워드 임베딩 \(Word Embedding\)

* 단어를 밀집표현 형태의 벡터로 표현하는 방법
* 워드 임베딩 과정을 통해 나온 벡터를 임베딩 벡터\(embedding vector\)라고 함
* Word2vec, Glove, FastText와 같은 방법론이 있음

| 원-핫 인코딩 | 워드 임베딩 |
| :--- | :--- |
| 고차원\(전체 단어 개수\) | 저차원, 사용자 지정 |
| 희소 벡터 | 밀집 벡터 |
| 1, 0으로 표현 | 실수로 표현 |
| 유사도 계산 불가능 | 유사도 계산 가능 |

### 희소 표현\(Sparse Representation\)

* 벡터 또는 행렬의 값이 대부분 0으로 표현되는 방법
* 원-핫 인코딩\(one-hot encoding\)방식

예시\) 1만개의 단어가 있고, 강아지의 인덱스는 5였을 때,   
 강아지 = \[ 0 0 0 0 1 0 0 0 0 0 0 0 … 중략 … 0\] \# 이 때 1 뒤의 0의 수는 9995개.

### 밀집표현\(Dense Representation\)

* 사용자가 설정한 값으로 모든 단어의 벡터 표현의 차원을 맞추는 방법
* 벡터의 차원이 조밀해졌다고 하여 밀집 벡터\(dense vector\)라고 함

예시\) 강아지 = \[0.2 1.8 1.1 -2.1 1.1 2.8 ... 중략 ...\] \(이 벡터의 차원은 128\)

## Word2Vec

* 비슷한 위치에서 등장하는 단어들은 비슷한 의미를 가진다라는 가정 \(강아지와 고양이는 비슷하다\)
* 중심 단어와 주변 단어로 학습하므로 라벨링이 필요 없음 -&gt; 비지도학습\(unsupervised learning\)
* CBOW\(Continuous Bag of Words\), Skip-gram 방식

### CBOW\(Continuous Bag of Words\) vs Skip-gram 방식

* CBOW : 주변에 있는 단어로부터 중심 단어를 예측
* Skip-gram : 중심 단어에서 주변 단어를 예측

### 네거티브 샘플링\(Negative Sampling\)

* 주변 단어-중심 단어 관계를 가지고 지정한 윈도우 사이즈 내에 존재하면 1, 그렇지 않으면 0으로 이진분류 문제로 변경하여 학습하면 더 빠르게 학습할 수 있음
* 전체 단어가 아니라, 일부에 대해서만 학습하도록 샘플링
* 여기서 원도우는 중심 단어를 예측하기 위해서 앞, 뒤로 몇 개의 단어를 볼지에 대한 범위이다 

### Word2Vec 모델 평가

* 코사인 유사도\(Cosine Similarity\)
  * 코사인 유사도는 두 특성 벡터 간의 유사 정도를 코사인 값으로 표현한 것
  * 코사인 유사도는 -1에서 1까지의 값을 가진다
  * '-1' 은 서로 완전히 반대, '0' 은 서로 독립, '1' 은 서로 같은 경우를 의미
* 유클리드 거리\(Euclidean Distance\)
* 자카드 유사도\(Jaccard Similarity
* Word Analogy
  * 유추를 통한 평가로 유추에 대한 데이터가 존재해야 테스트를 할 수 있음

## Glove

* 카운트 기반 방식은 단어 의미의 유추가 불가능, 예측 기반은 전체적인 통계 정보를 반영 못함
* GloVe는 이를 위해 카운트 기반과 예측 기반을 모두 사용
* 임베딩 된 중심 단어와 주변 단어 벡터의 내적이 전체 코퍼스에서의 동시 등장 확률이 되도록 만드는 것

## FastText

* Facebook research에서 공개한 단어 임베딩 기법
* 단어를 n-gram으로 나누어 학습
  * n-gram의 범위가 2-5로 설정한 경우 : assumption = {as, ss, su, …, ass, ssu, sum, …, mptio, ption, assumption}
* 실제 사용 시에는, 입력 단어가 사전에 있을 경우 해당 단어의 벡터를 곧바로 리턴하고 사전에 없는 경우 \(OOV, Out-of-Vocabulary\) 입력 단어의 n-gram vector를 합산하여 반환

## ELMo\(Embeddings from Language Model\)

* 문맥을 반영한 워드 임베딩 기법
* 글자가 같은 단어도 다른 뜻을 가지는 경우가 있음 \(바다 위에 '배'가 떠있다. 나무에 '배'가 열렸다.\)
* Pre-trained 모델의 시작

## Universal sentence encoder

* 구글이 공개한 pretrained model로 문장을 고차원 벡터로 인코딩
* 짧은 문장보다는 긴 문장에서 더 좋은 성능을 보임
* 여러가지 버전이 있으며, 한국어를 함께 지원하는 multilingual 버전이 존재
* 속도가 빠른 CNN 버전, 속도는 느리지만 성능이 더 뛰어난 Transformer 버전이 존재

