# tensorflow2x

## tensorflow \(version 2.x\)

## 텐서플로 2.x의 이해

: 텐서플로 2.x는 케라스\(keras\)와 같은 하이 레벨 API를 사용할 것을 권장하며, 내부의 세부정보를 더 많이 제어해야 하는 경우 텐서프롤 1.x인 로우레벨 API를 그대로 유지한다

## 즉시 실행 \(eager execution\)

: 텐서 플로 2.x은 텐서플로 1.x의 정적 계산 그래프를 정의한것과 다르게, 특별한 세션 인터페이스나 플레이스 홀더 업이도 노드를 즉시 정의, 변경, 실행할 수 있으며, 이것이 바로 즉시 실행이다 . 즉, 모델 정의가 동적이고 실행이 즉시 이뤄진다, 그래프와 세션은 구현 세부 사항으로 고려해야 한다

## 오토그래프\(AutoGraph\)

: 텐서 플로 2.x은 기본적으로 if-while, print\(\)과 같이 기본 특징과 같은 제어흐름을 포함해 명령형 파이썬 코드를 지원하여, 투명하고 역동적이며 즉시 실행 파이썬 형식 프로그래밍과 효율적인 그래프 계산을 통해 두세계를 모두 활용하는 연결고리를 만든다

* 오토 그래프 사용방법 

  : 파이썬 코드에 특정 데코레이터\(decorator\) tf.function을 어노데이션\(annotation\)처럼 써주기만 하면된다.

```python
import tensorflow as tf

def linear_layer(x):
  return 3 * x + 2

@tf.function
def simple_nn(x):
  return tf.nn.relu(linear_layer(x))

def simple_function(x):
    return 3*x
```

* simple\_nn을 살펴보면 텐서플로 내부와 상호작용하는 특수 핸들라는 것을 알수 있으며, simple\_function은 일반 파이썬 핸들러다.
* tf.function을 사용할 경우 하나의 주 함수에만 어노테이션을 달면 거기에서 호출된 다른 모든 함수는 자동으로 투명하게 최적화된 계산 그래프로 변환된다

```python
import  tensorflow as tf
import timeit

cell = tf.keras.layers.LSTMCell(100)

@tf.function
def fn(input, state):
    return cell(input, state)

input = tf.zeros([100, 100])
state = [tf.zeros([100, 100])] * 2
# warmup
cell(input, state)
fn(input, state)

graph_time = timeit.timeit(lambda: cell(input, state), number=100)
auto_graph_time = timeit.timeit(lambda: fn(input, state), number=100)
print('graph_time:', graph_time)
print('auto_graph_time:', auto_graph_time)
```

```text
graph_time: 0.09712530000000008
auto_graph_time: 0.0456865999999998
```

## 케라스 API : 3가지 프로그래밍 모델

* 케라스는 순차적 API, 함수적 API, 모델 서브클래싱의 세가지 프로그래밍 모델과 함께 더 하이레벨 API를 제공한다 

### 순차적\(Sequentail\) API

* 순차적 API는 90%의 사례에 적합한 매우 우아하고 직관적이며 간결한 모델이다. 

```text
tf.keras.utils.plot_model(model, to_file="model.png")
```

![sequentialAPI](../.gitbook/assets/sequentialAPI.png)

### 함수적\(function\) API

* 함수적 API는 다중 입력, 다중 출력, 비순차 흐름과의 잔존 연결, 공유, 재사용 가능 계층을 포함해 좀더 복잡한\(비선형\) 위상\(topology\)으로 모델을 구축하려는 경우 유용하다
* 각 계층은 호출 가능하고\(입력은 텐서\) 각 계층은 텐서를 출력으로 반환한다.
* 두개의 개별 입력, 두 개의 개별 로지스틱 회귀를 출력으로, 하나의 공유 모듈을 중간에 갖는 예제

```python
import tensorflow as tf

def build_model():
    # 가변 길이 정수의 시퀀스
    text_input_a = tf.keras.Input(shape=(None,), dtype='int32')

    # 가변 길이 정수의 시퀀스
    text_input_b = tf.keras.Input(shape=(None,), dtype='int32')

    # 1000개의 고유 단어를 128차원 벡터에 매핑해서 임베딩
    shared_embedding = tf.keras.layers.Embedding(1000, 128)

    # 양쪽 입력을 인코딩하고자 동일한 계층 재사용
    encoded_input_a = shared_embedding(text_input_a)
    encoded_input_b = shared_embedding(text_input_b)

    # 최종적으로 2개의 로지스틱 예측
    prediction_a = tf.keras.layers.Dense(1, activation='sigmoid', name='prediction_a')(encoded_input_a)
    prediction_b = tf.keras.layers.Dense(1, activation='sigmoid', name='prediction_b')(encoded_input_b)

    # 2개의 입력과 2개의 출력
    # 가운데는 모델이 있다.
    model = tf.keras.Model(inputs=[text_input_a, text_input_b], 
    outputs=[prediction_a, prediction_b])

    tf.keras.utils.plot_model(model, to_file="shared_model.png")

build_model()
```

* 비선형 위상의 예 

![functionAPI](../.gitbook/assets/functionAPI.png)

## 모델 서브클래싱

* 모델 서브클래싱은 최고의 유연성을 제공하며 일반적으로 자신의 계층을 정의해야 할 때 사용. 비유하자면 표준적이고 잘 알려진 레고 블록을 구성하는 대신 자신만의 레고 블록을 만들고자 할때 유용
* **init** : 선택적으로 이 계층에서 사용할 모든 하위 계층을 정의하는데 사용, 모델 선언을 할때는 생성자다
* build : 게층의 가중치를 생성할 때 사용, dd\_weight\(\)로 가중치를 추가 할 수 있다 
* call : 순반향 전달 정의, 계층이 호출되고 함수 형식으로 체인되는 곳이다
* 선택적으로 get\_config\(\)를 사용해 게층을 직렬화\(serialize\)할 수 있고, from\_config\(\)를 사용하면 역질렬화\(deserialize\)할 수 있다

## 콜백 \(callback\)

: 콜백은 훈련 중에 독작을 확장하거나 수정하고자 모델로 전달하는 객체

* ModelCheckPoint : 정기적으로 모델의 체크 포인트를 저장하고 문제가 발생할 때 복구하는데 사용 
* LearningRateScheduler : 최적화하는 동안 학습률을 동적으로 변경할 때 사용 
* EarlyStopping : 검증 성능이 한동안 개선되지 않을 경우 훈련을 중단할 때 사용 
* TensorBoard : 텐서보드를 사용해 모델의 행동을 모니터링할 때 사용 

## 모델과 가중치 저장

* 가중치를 텐서플로 체크포인트 파일로 저장 

```python
model.save_weight('./weigth/model') # 저장
model.load_weight(file_path) # 복원
```

* 가중치 이외의 모델은 JSON 형식으로 직렬화 할 수 있다 

```python
json_string = model.to_json() # 저장
model = tf.keras.model_from_json(json_string) # 복원
```

* YAML으로 직렬화 

```python
yaml_string = model.to_yaml() # 저장
model = tf.keras.model_from_yaml(yaml_string) # 복원
```

* 모델을 가중치와 최적화 매개변수와 함께 저장

```python
model.save('model.hs') # 저장
model = tf.keras.models.load_model('model.hs') # 복원
```

## 데이터셋 라이브러리

* 생성
  * from\_tensor\_slices\(\) : 개별\(또는 다중\) 넘파이\(또는 텐서\)를 받고 배치를 지원
  * from\_tensor\(\) : 1과 유사하지만 배치를 지원하지 않는다
  * from\_generator\(\) : 생성자 함수에서 입력을 취한다
* 변환
  * batch\(\) : 순차적으로 데이터셋을 지정한 크기로 분할
  * repeat\(\) : 데이터를 복제
  * shuffle\(\) : 데이터를 무작위로 섞는다 
  * map\(\) : 데이터에 함수를 적용
  * filter\(\) : 데이터를 거르고자 함수를 적요
* 반복
  * next\_batch = iterator.get\_next\(\)

