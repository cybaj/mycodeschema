---
layout: post
title: "c 함수, passing by pointer and reference"
categories: c
author: "김민석"
meta: "code schema"
---
## C에서도 call by value 가 default

Java 는 only call by value,
Python 은 call by object reference

C 에서 call by value 로 사용되는 경우, `const` 를 사용해주는 것이 좋아보인다.
```c
void add(int* body, const int operand)
{
    ...
}
```

## call by reference 를 할 때

**pointer**로 받거나 **reference**로 받을 수 있다.

**pointer** 로 하는 경우
```c
void swap(int* x, int* y) 
{ 
    int z = *x; 
    *x = *y; 
    *y = z; 
} 
```

**reference** 로 하는 경우
```c
void swap(int& x, int& y) 
{ 
    int z = x; 
    x = y; 
    y = z; 
} 
```

## 차이를 구분지어 보면

### 안정성에 영향을 줄 수 있는 차이
1. **pointer** 는 `NULL` 이 될 수 있지만, **reference** 는 그렇지 못하다.
2. **pointer** 는 **re-assign** 될 수 있지만, **reference** 는 그렇지 못하다.(**reference**는 초기화시 assign 되어야 한다.)

### pointer 가 편리해지는 경우가 있다
1. **array** 같은 경우, **pointer** 받는 것이 `*(array_ptr++)` 등 사용하는데 있어서 편리하다.

### 사용상의 단순 차이
1. class/struct 사용 시, **pointer** : `->`, **reference** : `.`
2. dereferencing 하는 경우, **pointer** : `*pointer` 가 값, **reference** : `some_lvalue` 가 값

## 무엇을 써야 할까

> Use references when you can, and pointers when you have to. But if we want to write C code that compiles with both C and a C++ compiler, you'll have to restrict yourself to using pointers.  *Rohit Kasle* 

[geeksforgeeks.org](https://www.geeksforgeeks.org/passing-by-pointer-vs-passing-by-reference-in-c/)

## Google C++ Style Guide

> Parameters to C/C++ functions are either input to the function, output from the function, or both. **Input** parameters are usually **values** or **const references**, while **output** and **input/output parameters** will be **non-const pointers**.

> In fact it is a very strong convention in Google code that input arguments are values or const references while output arguments are pointers.

## 정리하자면

*call site* 에서 보기 좋게, 어떤 것은 mutated 될 것이고, 어떤 것은 안 될 것인지 알기 쉽게.
```c
foo(x, y);     // x and y won't be mutated
bar(x, &y);    // y may be mutated
```
[Kerrek SB's answer](https://stackoverflow.com/questions/26441220/googles-style-guide-about-input-output-parameters-as-pointers)

*define*
```c
void foo(int a, const int &b);
void bar(int a, int *b);
```

C에서 함수의 매개변수는 3종류이고, 각각에 따른 convention 은 아래와 같다.
- *input* : **values** 나 **const reference** 로 받는다.
- *output* : **non-const pointers** 로 받는다.
- *input/output* : **non-const pointers** 로 받는다.

매개변수의 순서는 *input/output*, *output*, *input* 순서가 어떨까.

