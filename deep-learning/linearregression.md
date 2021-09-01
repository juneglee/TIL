# Linear Regression

## 선형 회귀 \(linear regression\)

: 가장 훌륭한 예측선 긋기

* 독립 변수 x 를 사용해 종속 변수 y의 움직임을 예측하고 설명하는 작업 
* x 값만으로도 y 값을 설명할 수 있을 때 단순 선형 회귀 \(simple linear regresssion\)
* x 값이 여러개가 필요할 때는 다중 선형 회귀 \(multiple linear regression\)
* 일차 함수 그래프의 식 Hypothesis : H\(x\) = Wx + b y = ax + b

## 최소 제곱법 \(method of least squares\)

: 정확한 직선을 긋을 수 있는 공식 ![methodOfLeastSquares](../.gitbook/assets/methodOfLeastSquares%20%281%29.png)

* x의 편차\(각 값과 평균과의 차이\)를 제곱해서 합한 값을 분모로 놓고, x와 y의 편차를 곱해서 합한 값을 분자로 놓으면 기울기가 나온다

  ex\) 공부량에 따른 성적을 예측 

TIP\) 최소 제곱법은 주어진 x의 값이 하나일 때 적용이 가능합니다. 여러 개의 x가 주어지는 경우 경사하강법을 이용한다

## 최소 제곱법을 이용한 선형 회귀

```python
import numpy as np

# x 값과 y값
x=[2, 4, 6, 8]
y=[81, 93, 91, 97]

# x와 y의 평균값 
# mean () : 모든 원소의 평균을 구하는 넘파이 함수 
mx = np.mean(x)
my = np.mean(y)
print("x의 평균값:", mx)
print("y의 평균값:", my)

# 기울기 공식의 분모
divisor = sum([(mx - i)**2 for i in x])
# sum()은 시그마에 해당하는 함수 이다 
# **2 는 제곱을 구하라는 의미 
# for i in x는 x의 각 원소를 한번씩 i 자리에 대입하라는 의미 

# 기울기 공식의 분자 : (x - x평균)*(y - y평균)의 합
def top(x, mx, y, my):
    d = 0
    for i in range(len(x)):
        d += (x[i] - mx) * (y[i] - my)
    return d
dividend = top(x, mx, y, my)

print("분모:", divisor)
print("분자:", dividend)

# 기울기와 y 절편 구하기
a = dividend / divisor
b = my - (mx*a)

# 출력으로 확인
print("기울기 a =", a)
print("y 절편 b =", b)
```

* 출력 값 

  x의 평균값: 5.0

  y의 평균값: 90.5

  분모: 20.0

  분자: 46.0

  기울기 a = 2.3

  y 절편 b = 79.0

## 평균 제곱 오차 \(mean square error: MSE\)

: 최소 제곱법을 이용해 가장 훌륭한 직선을 그렸지만, 여러 개의 입력을 처리하기에는 무리가 있다. 이렇게 여러개의 입력 값을 계산할 때는 임의의 선을 그리고 난 후, 이 선이 얼마나 잘 그려졌는지를 평가하여 조금씩 수정해 가는 방법을 사용한다. 이를위해 주어진 선의 오차를 평가하는 오차 평가 알고리즘이 필요하며, 평균 제곱 오차가 많이 사용된다.

* 임의의 직선을 그어 이에 대한 평균 제곱 오차를 구하고, 이 값\(오차\)을 가장 작게 만들어주는 a와 b 값을 찾아 가는 작업 

![MSE](../.gitbook/assets/MSE%20%281%29.png)

* y^는 x에 대응하는 '실제값'이고 y는 x가 대입되었을 때 직선의 방정식을 만드는 '예측값'이다.
* 예를 들어, 2시간 공부했을 때의 실제 나온 점수\(00점\)와 그래프 y = ax + b식에 x = 0 를 대입했을 때 \(00점\)의 차이를 오차라 한다 

## 평균 제곱 오차를 이용한 선형 회귀

* 리스트를 만들어 공부한 시간과 이에 따른 성적을 평균 제곱 오차를 이용

```python
import numpy as np

#가상의 기울기 a와 y 절편 b
fake_a_b=[3,76]

# x 값과 y값
data = [[2, 81], [4, 93], [6, 91], [8, 97]]
x = [i[0] for i in data]
y = [i[1] for i in data]

# y=ax + b에 a,b 값 대입하여 결과를 출력하는 함수
def predict(x):
   return fake_a_b[0]*x + fake_a_b[1]

# MSE 함수 (평균 제곱 공식) 
def mse(y, y_hat):
   return ((y - y_hat) ** 2).mean()
   # 예측값(y_hat)과 실제 값(y)을 각각 mse ()라는 함수의 y_hat와 y자리에 입력해서 평균 제곱을 구한다 

# MSE 함수를 각 y값에 대입하여 최종 값을 구하는 함수
def mse_val(predict_result,y):
   return mse(np.array(predict_result), np.array(y))

# 예측값이 들어갈 빈 리스트
predict_result = []

# 모든 x값을 한 번씩 대입하여 predict_result 리스트완성.
for i in range(len(x)):
   predict_result.append(predict(x[i]))
   print("공부시간=%.f, 실제점수=%.f, 예측점수=%.f" % (x[i], y[i], predict(x[i])))

# 최종 MSE 출력
print("MSE 최종값: " + str(mse_val(predict_result,y)))
```

출력값 공부시간=2, 실제점수=81, 예측점수=82 공부시간=4, 실제점수=93, 예측점수=88 공부시간=6, 실제점수=91, 예측점수=94 공부시간=8, 실제점수=97, 예측점수=100 MSE 최종값: 11.0

