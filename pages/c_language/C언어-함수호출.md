---
title: C언어 함수 호출 정리
keywords: C언어 함수, C언어 함수호출
last_updated: September 19, 2017
tags: [C언어]
summary: "C언어 함수 호출에 대한 정리입니다."
sidebar: c_language_sidebar
permalink: C언어-함수호출.html
folder: c_language
---

## 매개변수 전달방법

### call by value
---
값을 복사하며 전달하는 방법입니다. 값이 복사되므로 원본데이터에 손상이 안간다는 장점이 있지만 값의 복사로 인해 시간, 공간적 비용이 발생한다는 단점이 있습니다.

```
#include <stdio.h>

int simple_func(int num1, int num2){
    num1 = num1 + 1;
    num2 = num2 + 1;
    return num1 + num2;
}

int main()
{
    int n1 = 1, n2 = 2;

    printf("%d + 1 + %d + 1 = %d", n1, n2, simple_func(n1, n2));

    return 0;
}
출력 결과 : 1 + 1 + 2 + 1 = 5
```

num1과 num2에 1을 함수에서 더해도 원본 데이터인 n1과 n2에는 영향이 가지 않습니다. 값이 복사되었을 뿐, 둘은 전혀 다른 변수이기 때문입니다.

### call by reference
---
값의 주소를 전달하여 값 자체를 전달하는 방법입니다. 주소만 이동하므로 시간, 공간적 손해를 거의 안보지만 원본 데이터의 변형 우려가 있어 프로그램의 전체적인 복잡도가 증가한다는 단점이 있습니다.

```
#include <stdio.h>

int simple_func(int *num1, int *num2){
    *num1 = *num1 + 1;
    *num2 = *num2 + 1;
    return *num1 + *num2;
}

int main()
{
    int n1 = 1, n2 = 2;
    int answer = simple_func(&n1, &n2);

    printf("%d + %d = %d", n1, n2, answer);

    return 0;
}
출력 결과 : 2 + 3 = 5
```

## 재귀 함수

### 개요
---
자기 자신을 호출하는 방식으로 근본적으로 반복 + [스택](https://namu.wiki/w/스택(자료구조))이라고 보시면 됩니다. 같은 접근방식을 누적해가며 반복해야할 경우에 사용합니다. 대표적으로 피보나치의 수열, 하노이의 탑, 팩토리얼 등의 문제를 풀 때에 쓰입니다.

```
// 팩토리얼 예제
 unsigned int factorial(unsigned int n)
 {
     if (n <= 1)
         return 1;
     else
         return n * factorial(n-1);
 }
```

팩토리얼은 자기자신부터 1까지 순차적으로 곱해주어야합니다. 따라서 반복도 필요하고 값을 누적시킬 필요도 있습니다. 그래서 재귀함수로 쉽게 구현이 가능합니다.  

### 퍼포먼스 이슈
---
"재귀함수는 가독성이 좋지만 반복문에 비해 실행시간이 더 오래걸립니다."라고 보통 배웁니다. 하지만 C언어는 파이썬처럼 재귀 깊이가 995회정도로 제한적인것도 아니고 대부분의 컴파일러가 꼬리재귀 최적화를 제공하기 때문에 고려하지 않으셔도 됩니다. 구현체에 꼬리재귀(Tail Recursion) 최적화가 되어있는 경우 꼬리재귀 요청이 스택에 걸리는 대신 이전 실행지점으로의 점프로 작동 하므로 실질적으로 루프문과 유의미한 성능 차이는 없게됩니다.  
![tail_recursion](https://zerobugplz.github.io/images/studying/tail_recursion.png)  
스택을 한단계 더 쌓는게 아니라 이전 스택을 그대로 사용하게 되는 것으로 단순 재귀에만 해당됩니다(쉽게 이야기하면 재귀함수 안이 복잡하면 꼬리재귀가 일어나지 않습니다).

## 함수 호출 규칙

### 개요
---
주로 생략해버리지만 우리는 함수를 정의할 때에 호출 규칙을 정의할 수 있습니다. 호출 규칙으로 매개변수를 전달하는 순서, 매개변수가 사용한 메모리 관리방법등이 정의됩니다. 아래의 3가지 종류가 있습니다.

|---
| 호출 규칙 | 매개변수 스택정리 | 매개변수 메모리
| \_\_cdecl | Caller | Stack
| \_\_stdcall | Callee | Stack
| \_\_fastcall | Callee | Stack + Register

매개변수 스택 정리는 Caller이면 함수를 호출한 쪽에서 스택을 정리한다는 이야기이고 Callee이면 함수가 자체적으로 스택을 정리한다는 이야기입니다. 매개변수 메모리는 셋 다 스택을 사용하지만 fastcall은 특이하게 레지스터를 같이 사용합니다. 매개변수 복사를 레지스터에 넣어서 전달해주므로 약간 더 빠릅니다. 그럼 항상 fastcall을 쓰는게 좋느냐, 그건 컴파일러가 알아서 판단해서 최적화해줍니다.

### 정의
---
사실 이것은 반환형과 함수명 사이에 생략됐을 뿐 모든 함수에 정의되어 있습니다.

```
int 호출규칙 함수명(인자){내용}
```