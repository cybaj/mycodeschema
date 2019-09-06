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

`pointer`로 받거나 `reference`로 받을 수 있다.

`pointer` 로 하는 경우
```c
void swap(int* x, int* y) 
{ 
    int z = *x; 
    *x = *y; 
    *y = z; 
} 
```

`reference` 로 하는 경우
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
1. `pointer` 는 `NULL` 이 될 수 있지만, `reference` 는 그렇지 못하다.
2. `pointer` 는 **re-assign** 될 수 있지만, `reference` 는 그렇지 못하다.(`reference`는 초기화시 assign 되어야 한다.)

### pointer 가 편리해지는 경우가 있다
1. `array` 같은 경우, `pointer` 로 받는 것이 `*(array_ptr++)` 등 사용하는데 있어서 편리하다.

### 사용상의 단순 차이
1. class/struct 사용 시, pointer : `->`, reference : `.`
2. dereferencing 하는 경우, pointer : `*pointer` 가 값, reference : `some_lvalue` 가 값

## 무엇을 써야 할까

> Use **references** when you can, and **pointers** when you have to. But if we want to write C code that compiles with both C and a C++ compiler, you'll have to restrict yourself to using pointers. *Rohit Kasle* [geeksforgeeks.org][https://www.geeksforgeeks.org/passing-by-pointer-vs-passing-by-reference-in-c/]

