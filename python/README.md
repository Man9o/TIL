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

- numpy 가져오기


''' python
>>>import numpy as np # numpy를 np라는 이름으로 가져와라
'''
