# package

## Packages

: 패키지는 도트\(.\)를 사용하여 파이썬 모듈을 계층적\(디렉터리 구조\)으로 관리할 수 있게 한다

```text
number/
    __init__.py
    first/
        __init__.py
        echo.py
        wav.py
    second/
        __init__.py
        screen.py
        render.py
    third/
        __init__.py
        run.py
        test.py
```

## 패키지 안의 함수 실행하기

```python
import number.first.echo
>>> game.sound.echo.echo_test() # echo

from number.first import echo
>>> echo.echo_test() # echo

from number.first.echo import echo_test
>>> echo_test() # echo
```

## **init**.py 의 용도

: 해당 디렉터리가 패키지의 일부임을 알려주는 역할을 한다. 만약 패키지에 포함된 디렉터리에 **init**.py 파일이 없다면 패키지로 인식되지 않는다 \(단, python3.3 버전 부터는 **init**.py 파일 없어도 패키지로 인식한다 \)

* 이렇게 특정 디렉터리의 모듈을 \*를 사용하여 import할 때에는 다음과 같이 해당 디렉터리의 **init**.py 파일에 **all** 변수를 설정하고 import할 수 있는 모듈을 정의해 주어야 한다.
* 여기에서 **all**이 의미하는 것은 sound 디렉터리에서 \* 기호를 사용하여 import할 경우 이곳에 정의된 echo 모듈만 import된다는 의미

```text
C:/user/number/sound/__init__.py
__all__ = ['echo']
```

```python
rom game.sound import *
>>> echo.echo_test() # echo
```

## relative 패키지

: 서로 다른 디렉터리에 모듈을 사용할 수 있도록 만든다 relative한 접근자

* ..  부모 디렉터리
* .   현재 디렉터리

```python
# render.py
from ..sound.echo import echo_test
def render_test():
    print ("render") # echo_test()
```

