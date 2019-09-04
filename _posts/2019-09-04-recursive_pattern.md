---
layout: post
title: "recursive 겉모양"
categories: python
author: "김민석"
meta: "code schema"
---
## recursive는 문제 구조의 이해가 핵심이겠지만

짜다보니 어떤 틀이 있다는 생각이 들었다.  
틀을 외운다고 recursive 구조 파악을 잘하게 되는 것은 아니지만, 
코드로 옮길 때, 어떤 틀에 맞춰지는 것 같아서 간단히 남겨두자.

## recursive 함수의 겉모양

`iterator`와 `generator`를 발견했기 때문에, 반복문은 *"생성하는 성격"*, *"반복하는 성격"*으로 나누어 이해, 이용될 수 있다. 

```python
def some_recursive_f(body) :

    '''
    1. BASELINE PROCESS BLOCK
        A. CHECK : 결국 BASELINE 인지, 
        B. PROCESS : 그 경우에 어떤 처리를 하는지,
        C. RETURN : 무엇을 리턴할 것인지
    '''

    '''
    2. RECURSION BLOCK
        결국 *동일한 문제 구조* 아래 *보다 작은 문제* 를 무엇으로 보는지
        A. SET : 작은 문제 나누기
        A. INPUT : 이해에 따른 그 작은 문제의 INPUTs 은 무엇인지
        B. OUTPUT : BASELINE의 return == RECURSIVE stem block 여서 outputs이 잘 쌓여 나갈 수 있는지 결정
    '''

    '''
    +. MAKING RESULT
        A. RECURSION 결과를 통해 원하는 결과 만드는 부분
        B. RECURSION 의 결과가 그 자체로 함수의 result로 충분하지 않을 때, 고려될 수 있겠지만 불필요.
        C. 이 함수 내에서는 RECURSION 처리만을 하고 나머지는 함수 밖에서 처리하는 식이 자연스러움.
    '''
```

## 예제 recursive reverse

```python
def recursive_reverse_list(body):

    '''
    1. BASELINE PROCESS BLOCK
    '''
    if not isinstance(body, list):
        return [body]
    if not body:
        return body

    '''
    2. RECURSION BLOCK
    '''
    return recursive_reverse_list(body[-1]) + recursive_reverse_list(body[:-1])   
```
