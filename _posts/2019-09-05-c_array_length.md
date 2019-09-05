---
layout: post
title: "array를 입력 받는 함수에서 array length 이용하기"
categories: c
author: "김민석"
meta: "code schema"
---
## sizeof(array) / sizeof(array[0])

이 스니펫을 array의 length를 따질때 썼었다.

## 그런데 array 입력은 pointer 입력으로 바뀐다

array 입력  
```c
void foo(int a[])
{
    // ...
}
```

pointer 입력
```c
void foo(int *a)
{
    // ...
}
```

## 따라서 함수 내에서 array의 length를 따질 수 없다

만약 해당 함수 내에서 array length 를 위 스니펫을 사용하면, 아래 에러가 나온다.

```
sizeof on array function parameter will return
      size of 'int *' instead of 'int []' [-Wsizeof-array-argument]
```

## 따라서 array에, 길이값까지 매개변수에 추가하여 사용한다

```c
void input_array_f(size_t sz, int *arr){
    // ...
}
```

