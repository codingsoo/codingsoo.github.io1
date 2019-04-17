---
title: C언어 전처리기에 대한 이야기
keywords: C언어 전처리기, C언어 매크로, define
last_updated: September 19, 2017
tags: [C언어]
summary: "C언어 전처리기에 대한 이야기"
sidebar: c_language_sidebar
permalink: C언어-전처리기.html
folder: c_language
---

## 전처리기

컴파일하기 전에 앞서서 소스 코드를 변형하는 컴파일러의 한 부분입니다. 소스파일중 미리 처리해달라는 키워드가 있다면 미리 처리해서 임시파일을 생성하고 그 후 컴파일이 되는 것입니다.  

```
#define 매크로 정의
#include 파일 포함
#undef 매크로 정의 해제
#if 조건이 참일 경우
#else 조건이 거짓일 경우
#endif 조건 처리 문장 종료
#ifdef 매크로가 정의되어 있는 경우 
#ifndef 매크로가 정의되어 있지 않은 경우 
#line 행번호 출력
#pragma 시스템에 따라 의미가 다름
```

## 매크로

매크로는 컴퍼일러에게 코드의 특성을 알려주는 키워드입니다. 따라서 기계어로 컴파일 과정에서 필요한 요소이고, 매크로 자체가 기계어 코드로 생성되지는 않지만 특정 코드를 제어하는데 사용됩니다. 몇개만 살펴보겠습니다.  

### 단순 매크로
---
숫자상수를 기호상수로 만들어주는 단순매크로입니다.  
  
아래의 코드에서는 define매크로에 의해 PI를 3.14로 전부 바꾸어줍니다. 프로그램의 가독성을 높여주고 상수의 변경이 용이하다는 장점이 있습니다. 숫자 외에도 &&, \|\| 등도 올 수 있습니다.  

```
#include <stdio.h>

#define PI 3.14

int main(void)
{

    printf("%f",PI);

    return 0;
}
출력 결과:
3.14
```

### 함수 매크로
---
매크로가 함수처럼 매개 변수를 갖는 것을 함수 매크로라고 합니다.  
  
연산자 우선순위를 고려하지 않게 하기 위해서 괄호로 잘 감싸주어야 합니다. 함수 호출 단계가 필요없어 실행속도가 빠르다는 장점이 있습니다.

```
#include <stdio.h>

#define SQUARE(x) ((x)*(x))

int main(void)
{

    printf("%d",SQUARE(5));

    return 0;
}
출력 결과 : 
25
```

### 인라인 함수
---
인라인 함수는 함수를 선언할 때 inline 키워드를 붙입니다. 인라인함수는 매크로함수의 장점은 그대로 살리면서도 자료형 문제, 괄호 문제, 제어문 문제, 지역변수 문제 등 다양한 문제를 해결하였습니다.
```
inline 반환값자료형 함수이름(매개변수자료형 매개변수이름)
{
}
```

함수와 매우 비슷하지만 인라인 함수는 컴파일러가 해당 함수를 직접 코드 안에 붙여넣어줍니다. 따라서 함수를 호출하지 않는 만큼 속도가 조금 더 빠릅니다. 하지만 함수를 복사해서 붙여 넣으므로 실행파일은 좀 더 크기가 커집니다. 두 수를 더하는 프로그램으로 예를 들어보겠습니다.

```
#include <stdio.h>

inline int add(int a, int b)
{
    return a + b;
}

int main()
{
    int num;

    num = add(1, 2); // 이 부분이 컴파일러에 의해 num = inline int(1,2){return 1+2;}로 바뀜

    printf("%d\n", num);  // 30

    return 0;
}
```

인라인 함수는 사용을 해도 컴파일러가 판단했을 때 너무 부적절하면 인라인 처리를 안합니다.  
그리고 비주얼 스튜디오 같은 IDE에서는 인라인함수 검사하기 기능이 있어서 모든 함수를 검사하여 인라인 함수를 사용하는 것이 효율적이라면 인라인함수로 변경해줍니다.

### #연산자
---
샾이 붙으면 해당 내용을 문자열로 변경합니다.

```
#include <stdio.h>
#define STRING(abc) #abc

int main()
{
    int a = 10;

    printf("%s",STRING(tyu));

    return 0;

}
```

### ##연산자(토큰 병합 연산자)
---
token-pasting operator(토큰 병합 연산자) ##연산자  

```
#define U(a,b) a##b
코드에서 U(x,1)이라고 썻다면 그 자리를 x1로 대체합니다.
```

### 내장 매크로

미리 정의된 매크로입니다.

```
#include <stdio.h>

int main(void)
{

    printf("%s\n",__DATE__);

    return 0;
}
출력 결과:
May  9 2017
```

```
__DATE__ => 이 매크로를 만나면 현재의 날짜(월 일 년)로 치환됨
__TIME__ => 이 매크로를 만나면 현재의 시간(시:분:초)으로 치환됨
__LINE__ => 이 매크로를 만나면 현재의 라인 번호로 치환됨
__FILE__ => 이 매크로를 만나면 현재의 소스 파일 이름으로 치환됨
```

### ASSERT 매크로
---
assert 매크로의 인자는 항상 True가 되는 조건식을 넣어줍니다. 만약 false인 경우는 문제가 발생했음을 사용자에게 알려주게 됩니다. 즉, assert(1) 인 경우는 무사 통과하고 assert(0) 인 경우는 문제 발생합니다.  

### 조건부 컴파일 지시
---
어떤 조건이 만족되었을 경우에만 컴파일하는 조건부 컴파일 지시입니다. 주로 헤더파일의 중복을 막기 위해 사용됩니다.  

```
#include <stdio.h>

#define MAC

int main(void)
{
#ifdef MAC // MAC이 정의되었을 경우
    printf("MAC\n");
#else // 정의 되지 않았을 경우
    printf("WINDOW\n");
#endif // 끝마침
    return 0;
}
출력 결과:
MAC
```

위의 ifdef와 반대되는 ifndef도 있습니다.

```
#include <stdio.h>

int main(void)
{
#ifndef MAC
    printf("WINDOW\n");
#else
    printf("MAC\n");
#endif
    return 0;
}
출력 결과:
WINDOW
```

파일들이 많이 분할되다보면 헤더파일들이 중복 포함되는 경우가 있습니다. 이를 방지하기 위해 아래와 같이 많이 합니다.

```
#ifndef __DEFINE__H_
#define __DEFINE__H_

#include <stdio.h>

int main(void)
{
    // 내용
    
    return 0;
}

#endif
```

위의 헤더파일이 include 되면 __DEFINE__H_가 정의되고 다음부터는 ifndef로 인해 다시 이 헤더파일이 중복 포함되지 않게 됩니다.

### #pragma once
---
위와 마찬가지로 헤더파일의 중복 선언을 막기위해 선언하는 것입니다. ifndef나 pragma once중에 하나를 선택해서 쓰시면 됩니다.

```
#pragma once

// 코드
```

### 매크로의 정의 취소하기
---
```
#undef HI // HI 매크로의 정의를 취소합니다.
```