# logistic regression

### 로지스틱 회귀 (logistic regression)
: 참인지 거짓인지를 구분
- 참(1) 과 거짓(0) 사이를 구분하는 s자 형태의 선을 그어 주는 작업

### 시그모이드 함수 
![sigmoidfunction](../../img/DL/sigmoidfunction.png) <br>
- a는 그래프의 경사도를 결정, a가 커지면 경사가 커지고, a 값이 작아지면 경사가 작아진다 
- b는 그래프의 좌우 이동을 의미, b 값이 클 때 좌로 이동, b 값이 작아질 때 우로 이동
- a와 b의 값에 따라 오차가 변하며, a 값이 작아지면 오차는 무한대로 커진다.
- 그런데 a 값이 커진다고 해서 오차가 무한대로 커지지는 않는다 
- 시그모이드 함수에서 a와 b의 값을 구하는 방법은 경사 하강법이다 
- 실제값에 따라 예측값에 가까워 지면 오차가 커지게 되는데, 이때 공식은 로그 함수를 이용한다 

### 로그 함수 
![logfunction](../../img/DL/logfunction.png) <br>
- 실제 값이 1일 때 -logh 그래프를 쓰고, 0일 때는 -log(1 - h)그래프를 써야 한다 
- 실제 값이 y 일 때, 이 값이 1이면, 오른쪽 부분의 없이지고,
- 반대로 0이면 왼쪽 부분이 없어져서 실제 값에 따라서 그래프가 변한다 

### 코딩으로 확인하는 로지스틱 회귀
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

#공부시간 X와 성적 Y의 리스트를 만듭니다.
data = [[2, 0], [4, 0], [6, 0], [8, 1], [10, 1], [12, 1], [14, 1]]

x_data = [i[0] for i in data] # 공부시간
y_data = [i[1] for i in data] # 성적

#그래프로 나타내 봅니다.
plt.scatter(x_data, y_data)
plt.xlim(0, 15)
plt.ylim(-.1, 1.1)

# 기울기 a와 절편 b의 값을 초기화 합니다.
a = 0
b = 0

#학습률을 정합니다.(임의로 정함)
lr = 0.05 

#시그모이드 함수를 정의합니다.
def sigmoid(x):
    return 1 / (1 + np.e ** (-x))

#경사 하강법을 실행합니다.
for i in range(2001):
    for x_data, y_data in data:
        a_diff = x_data*(sigmoid(a*x_data + b) - y_data)  # a에 관한 편미분, 앞써 정의한 sigmoid 함수 사용
        b_diff = sigmoid(a*x_data + b) - y_data           # b에 관한 편비분
        a = a - lr * a_diff                               # a를 업데이트 하기 위해, a_diff에 학습률을 lr을 고합 값을 a에서 뻄 
        b = b - lr * b_diff                               # b를 업데이트 하기 위해, b_diff에 학습률을 lr을 고합 값을 b에서 뻄 
        if i % 1000 == 0:    # 1000번 반복될 때마다 각 x_data값에 대한 현재의 a값, b값을 출력합니다.
            print("epoch=%.f, 기울기=%.04f, 절편=%.04f" % (i, a, b))


# 앞서 구한 기울기와 절편을 이용해 그래프를 그려 봅니다.
plt.scatter(x_data, y_data)
plt.xlim(0, 15)
plt.ylim(-.1, 1.1)
x_range = (np.arange(0, 15, 0.1)) #그래프로 나타낼 x값의 범위를 정합니다.
plt.plot(np.arange(0, 15, 0.1), np.array([sigmoid(a*x + b) for x in x_range]))
plt.show()
```

```
epoch=0, 기울기=-0.0500, 절편=-0.0250
epoch=0, 기울기=-0.1388, 절편=-0.0472
epoch=0, 기울기=-0.2268, 절편=-0.0619
epoch=0, 기울기=0.1201, 절편=-0.0185
epoch=0, 기울기=0.2374, 절편=-0.0068
epoch=0, 기울기=0.2705, 절편=-0.0040
epoch=0, 기울기=0.2860, 절편=-0.0029
epoch=1000, 기울기=1.4978, 절편=-9.9401
epoch=1000, 기울기=1.4940, 절편=-9.9411
epoch=1000, 기울기=1.4120, 절편=-9.9547
epoch=1000, 기울기=1.4949, 절편=-9.9444
epoch=1000, 기울기=1.4982, 절편=-9.9440
epoch=1000, 기울기=1.4984, 절편=-9.9440
epoch=1000, 기울기=1.4985, 절편=-9.9440
epoch=2000, 기울기=1.9065, 절편=-12.9489
epoch=2000, 기울기=1.9055, 절편=-12.9491
epoch=2000, 기울기=1.8515, 절편=-12.9581
epoch=2000, 기울기=1.9057, 절편=-12.9514
epoch=2000, 기울기=1.9068, 절편=-12.9513
epoch=2000, 기울기=1.9068, 절편=-12.9513
epoch=2000, 기울기=1.9068, 절편=-12.9513
```
![logisticregression](../../img/DL/logisticregression.png) <br>

-만약 여기에 입력 값이 추가되어 세개 이상의 입력 값을 다룬다면, 시그모이드 함수가 아니라 소프트맥스 (softmax)라는 함수를 써야 한다 
