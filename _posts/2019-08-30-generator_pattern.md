---
layout: post
title: "generator 일반적으로 사용하기"
categories: python
author: "김민석"
meta: "code schema"
---
## Generator 란

1. `yield`를 이용하여 함수를 정의한다.
2. 이 함수는 `iterator`를 리턴한다.
3. 이 함수가 `generator`다.
4. 사용의 요는 `yield` 구문에서 `next()`로 값을 받고, 그 상태로 유지되며, 다음 `next()`는 `yield` 구문 이후부터 시작된다.
5. (메모리 활용 상 이점이 있다.)

집중하고자하는 것은 편리함.
**4.** 덕에 절차적인 코딩이 된다.

## 따라서 절차적으로 쓰기 좋다

`iterator`와 `generator`를 발견했기 때문에, 반복문은 *"생성하는 성격"*, *"반복하는 성격"*으로 나누어 이해, 이용될 수 있다. 

```python
for i in range(10):
    if i % 2 :
        pass
    else if i % 3 :
        pass
    else if i % 5 :
        pass
    else if i % 7 :
        pass
```
위와 같은 반복문 안의 많은 조건문을 두어 *절차적 처리*를 하였었는데, 이런 식인 코드 형태는 *처리의 절차성*이 잘 나타나지 않는다. (그것보다도 저런 식으로 코딩할 때, 깔끔하게 하는 것은 *수학적 고민*이 많이 필요하고, 그렇게 고민 않고 코딩하면 코딩하기가 싫다.)

`generator`를 사용하면, *절차성*이 잘 나타난다.
이를테면 이렇게 할 수 있다.

```python
def my_generator():
    # 먼저 0, 1, 2
    for i in range(3):
        yield i
    # 그 다음에 1000
    yield 1000
    # 그 다음에 4,5,6,7
    for i in range(4,8):
        yield i
    # 마지막으로 0
    yield 0
```

위와 같은 식으로 `generator`는 *하나의 절차*=*작은 절차*+*반복된 절차일 수도 있고*+*종결과 같은 역할을 맡은 절차일 수도 있고*

## 일반적으로 while을 사용하는 것이 원자적으로 느껴진다

아래와 같은 '코드 스키마'를 외우자.

```python
def my_while_generator():
    # 1.상태에 대한 index, '_i'
    _i = 0
    # 2.subprocedures property
    _l_s = [num_a, numb_b, num_c, ..]
    # 3.그 중 첫번째 '작은 절차'
    while _i < num_a:
        yield "something" #4.'작은 절차' 내 yield
        i += 1 # 4.yield 할 때 마다 상태 index, '_i'를 늘린다.
    # ... 그 다음 '작은 절차'
```

