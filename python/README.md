# 파이썬

---

- Python의 철학 (Zen of Python)
  - 아름다운 것이 추한 것보다 낫다. (Beautiful is better than ugly)
  - 명시적인 것이 암시적인 것보다 낫다. (Explcit is better than implicit)
  - 간결한 것이 복잡한 것보다 낫다. (Simple is better than complex)

- 파이썬의 특징
  - 파이썬은 인간다운 언어이다.
  - 파이썬은 문법이 쉬워 빠르게 배울 수 있다.
  - 파이썬은 무료이지만 강력하다.
  - 파이썬은 간결하다.
  - 파이썬은 개발 속도가 빠르다. (Life is too short, You need python.)
  
---
## 숫자형 자료형

- 숫자형 : 숫자형(Number)이란 숫자 형태로 이루어진 자료형으로, 우리가 이미 잘 알고 있는 것들이다.
  - 정수형 : 정수형(Integer)이란 말 그대로 정수를 뜻하는 자료형을 말한다. 다음 예는 양의 정수와 음의 정수, 숫자 0을 변수 a에 대입하는 예이다.
  
```python
>>> a = 123
>>> a = -123
>>> a = 0
```

  * 실수형 : 파이썬에서 실수형(Floating-point)은 소수점이 포함된 숫자를 말한다. 다음 예는 실수를 변수 a에 대입하는 예이다.
  
```python
>>> a = 1.2
>>> a = -3.45
>>> a = 4.24E10
>>> a = 4.24e-10
```

  - 8진수와 16진수
    - 8진수는 숫자가 0O(소문자 혹은 대문자)로 시작하면 된다.

```python
>>> a = 0o177
```

   * 16진수는 0x로 시작하면 된다.

```python
>>> a = 0x8ff
```

  - 사칙연산
    - x의 y제곱을 나타내는 ** 연산자

```python
>>> a = 3
>>> b = 2
>>> a ** b
9
```

   * 나눗셈 후 나머지 반환 % 연산자

```python
>>> 5 % 2
1
```

   - 나눗셈 후 몫을 반환하는 // 연산자

```python
>>> 15 // 2
7
```

## 문자열 자료형

- 문자열 : 문자열(String)이란 문자, 단어 등으로 구성된 문자들의 집합을 의미한다.

"Life is too short, You need Python" <br>
"a" <br>
"123" <br>


---
## numpy

numpy는 과학 계산을 위한 라이브러리로서 다차원 배열을 처리하는데 필요한 여러 유용한 기능을 제공하고 있다.

#### numpy 가져오기


~~~python
import numpy as np # numpy를 np라는 이름으로 가져와라
~~~

#### numpy 배열 생성하기
넘파이 배열을 만들때는 mp.array() 메서드를 이용한다. np.array()는 파이썬의 리스트를 인수로 받아서 (numpy.ndarray)로 반환한다.


~~~python
>>> x = np.array([1.0, 2.0, 3.0])
>>> print(x)
[1. 2. 3.]
>>> type(x)
<class 'numpy.ndarray'>
~~~

#### numpy 산술 연산

원소의 수가 같을 경우 산술 연산이 각 원소에 대해서 행해진다.
원소의 수가 다르면 오류가 발생
원소별 계산뿐 아니라 넘파이 배열과 수치 하나(스칼라값)의 조합으로 산술연산이 가능한데, 이 기능을 **브로드캐스트**라고 한다.

~~~python
>>> x = np.array([1.0, 2.0, 3.0])
>>> y = np.array([2.0, 4.0, 6.0])
>>> x + y # 원소별 덧셈
array([3., 6., 9.])
>>> x - y # 원소별 뺄셈
array([-1., -2., -3.])
>>> x * y # 원소별 곱셈
array([2., 8., 18.])
>>> x / y # 나누어서 몫을 반환
array([0.5, 0.5, 0.5])

>>> x = np.array([1.0, 2.0, 3.0])
>>> x / 2.0
array([0.5, 1., 1.5,])
~~~

#### numpy의 N차원 배열

넘파이는 1차원 배열뿐 아니라 다차원 배열도 작성이 가능하다.
~~~python
>>> A = np.array([[1,2], [3,4]])
>>> print(A)
[[1 2]
 [3 4]]
>>> A.shape
(2, 2)
>>> A.dtype
dtype('int64')
>>> B = np.array([3,0],[0,6])
>>> A + B
array([[4, 2],
       [3, 10]])
>>> A * 10 # 브로드캐스팅 기능
array([[10, 20],
       [30, 40]]) 
~~~

넘파이 배열은 N차원 배열을 작성할 수 있는데 수학에서는 1차원 배열은 **벡터**, 2차원 배열은 **행렬** 이라고 하며 벡터와 행렬을 일반화 한것을 **텐서**라고 한다.

#### 브로드캐스트

형상이 다른 배열끼리의 연산을 가능하게 한다.

~~~python
>>> A = np.array([[1, 2], [3, 4]])
>>> B = np.array([10 , 20])
>>> A * B
array([[ 10, 40],
       [ 30, 80]])
~~~

#### 원소 접근

~~~python
>>> X = np.array([[51, 55], [14, 19], [0, 4]])
>>> print(X)
[[51 55]
 [14 19]
 [ 0  4]]
>>> X[0]           # 0행
array([51, 55])
>>> X[0][1]        # (0,1) 위치의 원소
55
~~~

for 문으로도 각 원소에 접근이 가능하다.

~~~python
>>> for row in X:
        print(row)
        
[51 55]
[14 19]
[0 4]

>>> X = X.flatten()          # X를 1차원 배열로 변환(평탄화)
>>> print(X)
[51 55 14 19 0 4]
>>> X[np.array([0, 2, 4])]   # 인덱스가 0, 2, 4인 원소 얻기
array([51, 14, 0])

>>> X > 15
array([ True, True, False, True, False, False], dtype=bool)
>>> X[X>15]
array([51, 55, 19])          # X중에서 값이 15보다 큰 값만 꺼낼 수 있다.
~~~

## matplotlib

딥러닝 실험에서는 그래프 그리기와 데이터 시각화도 중요하다. **matplotlib**은 그래프를 그려주는 라이브러리이다.

#### 단순한 그래프 그리기
그래프를 그리려면 matplotlib의 **pyplot** 모듈을 이용한다.


~~~python
import numpy as np
import matplotlib.pyplot as plt

# 데이터 준비
x = np.arange(0, 6, 0.1)  # 0에서 6까지 0.1 간격으로 생성
y = np.sin(x)

# 그래프 그리기
plt.plot(x, y)
plt.show()  # 호출
~~~
<img width="292" alt="image" src="https://user-images.githubusercontent.com/38044331/60781815-d7cd0680-a17e-11e9-846b-15a03e3351f4.PNG">

#### pyplot의 기능

sin함수와 cos함수, 제목과 각 축의 이름(레이블) 표시 등이 가능하다.

~~~python
import numpy as np
import matplotlib.pyplot as plt

# 데이터 준비
x = np.arange(0, 6, 0.1) # 0에서 6까지 0.1 간격으로 생성
y1 = np.sin(x)
y2 = np.cos(x)

# 그래프 그리기
plt.plot(x, y1, label="sin")
plt.plot(x, y2, linestyle="--", label="cos") # cos 함수는 점선으로 그리기
plt.xlabel("x") # x축 이름
plt.ylabel("y") # y축 이름
plt.title('sin & cos') # 제목
plt.legend()
plt.show()
~~~
<img width="310" alt="image1" src="https://user-images.githubusercontent.com/38044331/60782262-ec120300-a180-11e9-884d-77edeebbb6a8.PNG">

