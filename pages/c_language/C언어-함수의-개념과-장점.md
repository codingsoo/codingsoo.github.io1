---
title: C언어 함수의 개념과 장점
keywords: C언어 모듈화, C언어 함수
last_updated: September 19, 2017
tags: [C언어]
summary: "C언어 함수에 대한 소개입니다."
sidebar: c_language_sidebar
permalink: C언어-함수의-개념과-장점.html
folder: c_language
---

# 함수

## 모듈 == 함수

### 모듈의 개념
---
- 모듈 : 독립되어 있는 프로그램의 일부분
- 모듈러 프로그래밍 : 모듈 개념을 사용하는 프로그래밍 기법
- C언어에서는 모듈 == 함수

### 모듈러 프로그래밍의 장점
---
모듈러 프로그래밍은 요즈음 대세 프로그래밍 기법입니다.  

1. 각 모듈은 독자적으로 개발 가능(협업시 유리)
2. 다른 모듈과 독립적으로 수정이 가능(협업시 유리)
3. 유지보수가 쉽고 오류 찾기가 수월함
4. 모듈의 재사용 가능

### 함수의 개념과 장점 예시
---
- 함수(function): 특정한 작업을 수행하는 독립적인 부분
- 함수 호출(function call): 함수를 호출하여 사용하는 것

우리가 항상 보는 int main(){}도 함수입니다. C언어에서 프로그램은 여러개의 함수로 이루어지고 함수 호출을 통하여 서로서로 연결됩니다. 가장 먼저 호출되는 함수는 항상 main함수입니다.   

함수를 사용하는 것과 사용하지 않는 것의 비교를 해보겠습니다. 누가 로그인을 하면 환영 메세지를 보내는 프로그램을 만든다고 가정해보겠습니다.  

```
#include <stdio.h>

int main() {
    printf("qweqr님 안녕하세요!\n");
    printf("sadfds님 안녕하세요!\n");
    printf("asdfsa님 안녕하세요!\n");
    printf("gege님 안녕하세요!\n");
    return 0;
}
```

함수를 사용해서 짜보도록 하겠습니다. 실행 순서는 main함수부터 시작해서 GreetUser함수를 만나면 GreetUser함수 부분으로 점프를 뛰어서 실행시키고 다시 main함수에서 호출했던 곳으로 돌아오는 식으로 실행됩니다. printf처리 하는 부분이 따로 작성되어 main함수 부분이 더 단순해졌고 main에서 님 안녕하세요!를 따로 작성할 필요가 없어서 더 쉬워졌습니다.  

```
#include <stdio.h>

void GreetUser(char name[])
{
    printf("%s님 안녕하세요!\n");
}

int main() {
    GreetUser("qweqr");
    GreetUser("sadfds");
    GreetUser("asdfsa");
    GreetUser("gege");
    return 0;
}
```

이 경우에는 워낙 함수의 길이가 짧아서 특성이 잘 드러나지 않을 수 있습니다. 하지만 코드가 길어지면 길어질수록 함수를 한 번만 잘 짜놓으면 main에서 손쉽게 여러번 쓸 수 있다는 것은 느낄 수 있겠죠? 재사용성 뿐만 아니라 독립적으로 함수를 구현해 놓으므로서 각 함수를 서로 따로 개발하기가 용이하고 오류가 났을 경우에도 수정하기가 훨씬 편해집니다.  

### 함수의 이름
---
함수의 이름은 주소값을 갖습니다. 
```
#include <stdio.h>

int main(void)
{
    int *ptr = reinterpret_cast<int *>(main);

    printf("%p == %p",ptr,main); # 0x104abff40 == 0x104abff40

    return 0;
}
```

### 함수의 종류와 구성요소
---
함수는 크게 사용자 정의 함수와 라이브러리 함수로 나뉘게 됩니다.  

- 라이브러리 함수 : printf, scanf같이 이미 만들어져서 기본으로 컴파일러가 제공하는 함수를 말합니다.  
- 사용자 정의 함수 : 개발자가 직접 정의한 함수를 말합니다.  

함수의 구성요소는 크게 아래와 같이 나뉩니다.  

- 반환형 : 반환할 데이터 타입으로 맨 앞에 옵니다.
- 함수 이름 : 함수의 이름으로 반환형 다음에 옵니다.
- 매개 변수 : 외부에서 전달되는 변수로 필수사항은 아닙니다. 매개변수가 없을 경우 비워두거나 void라고 표시해줍니다. 여러개가 올수도 있습니다.
- 함수 몸체 : 함수의 기능을 작성합니다. 반환형이 void가 아닐 경우 각 반환형에 맞는 자료형으로 return 해주어야 합니다. return 값은 반드시 한개만 올 수 있습니다.

예시 : n! 구하기 함수 
 
```
int factorial(int n) // 반환형 int, 함수 이름 factorial, 매개변수 int형 변수 n 
{
    int i; // 함수 내의 지역변수로 함수 안에서만 사용 가능
    int result = 1;

    for(i = 1; i <= n; i++)
        result *= i;

    return result; // result 값을 반환(int 형)
}
```

### 함수 작성 위치
---
보통 함수는 main함수의 뒤쪽에 작성합니다. 그 대신 main함수의 앞쪽에 함수 원형을 호출하여 컴파일러에게 해당 함수가 올 것임을 알려주어야 합니다.  


```
#include <iostream>

int factorial(int n);

int main() {
    printf("5! = %d",factorial(5));

    return 0;
}

int factorial(int n) // 반환형 int, 함수 이름 factorial, 매개변수 int형 변수 n
{
    int i; 
    int result = 1;

    for(i = 1; i <= n; i++)
        result *= i;

    return result; // result 값을 반환(int 형)
}
```