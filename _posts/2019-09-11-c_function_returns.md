---
layout: post
title: "c 함수, returns by pointer and reference"
categories: c
author: "김민석"
meta: "code schema"
---
## 단순히 값을 반환하느냐, 수정한 것을 반환하느냐

값을 반환한다면 쉽고,  
  
**pointer** 나 **reference** 로 받아서  
1. 수정하고 그 처리 결과를 반환하거나,  
2. 수정하고 수정된 값으로 반환하거나,  
3. 수정하고 수정된 것을 그대로 반환할 수 있을텐데,  

`1.`, `2.`의 경우는 그대로 그냥 하면 되고,  
고민이 되는 것은 `3.`의 경우,  
**pointer** 로 returns 해야 하는가, **reference** 로 리턴해야 하는가.


**pointer**
```c
int* add(int* body, const int operand)
{
    ...
}
```

**reference**
```c
int& add(int* body, const int operand)
{
    ...
}
```

## 큰 차이는 `nullable`

**pointer**는 `null`이 될 수 있으나, **reference**는 선언과 동시에 초기화되기 때문에 그렇지 못하고.

## 어느 것으로 하든 별 상관없다는 의견

> Speedup - no difference. Readability - probably a slight advantage for references, no derefencing in the upstack code.

[Seva Alekseyev's answer](https://stackoverflow.com/a/5542003/6764514)

## 단, 단순히 값을 리턴 받는 경우라면 pointer를 지양하자는 의견 

> There's no benefit I can think of in returning a pointer to an integer from a property-type method such as getWidth(). It adds the burden of having to track memory ownership; but is actually likely to increase the bandwidth of the return type (both int and pointer sizes are platform specific, and can and do vary, but typical sizes are 32 and 64 bits respectively).

[Jim Blackler's answer](https://stackoverflow.com/a/5542026/6764514)

## unclear ownership

> Ownership may be more unclear when you return a pointer.

[Erik's answer](https://stackoverflow.com/a/5541977/6764514)

**pointer**를 사용하는 경우에는 `ownership`이 불분명해진다는 의견.  
생각해보면, **pointer**를 사용하는 곳이 `ownership`을 가지고 있는 context라고 여기고, 나머지는 **reference**로 다룬다면,  
좀 더 분명하게 코딩할 수 있지 않을까.

## Pointer ownership 

> I don't think there is a universally accepted, 100% accurate and always-applicable definition, but the most useful definition of ownership I've encountered in the context of C++ (and programming in general) is responsibility for cleanup. That is, an owner of a resource is the one who's responsible for correct cleanup of that resource.

[Angew's answer](https://stackoverflow.com/a/49025071/6764514)

## 정리

우선 단순 값을 리턴하는 경우를 제외하고, input 으로 들어온 수정된 값을 리턴 하는 경우에서,  
**pointer**로 리턴하거나, **reference**로 리턴할 수 있는데, 그 결정은 아래 내용을 참고하자.   

만약 리소스에 대한 소유권이 있는 context 내에서는 함수 처리가 사용된다면 **pointer** 를 받고, 나머지 경우에는 **reference** 로 받는 것이 좋아보임.  
그리고 **pointer**는 nullable 함을 인지하며 작업.  
