---
title: C언어 조건문
keywords: C언어 조건문, if문, switch문
last_updated: September 17, 2017
tags: [C언어]
summary: "C언어 조건문에 대한 이야기"
sidebar: c_language_sidebar
permalink: C언어-조건문.html
folder: c_language
---

## 조건문

### 개요
---
조건문이란 조건에 따라 다른 결과물을 보여주고 싶을 때 사용합니다. 예를들어 테트리스 게임을 만든다고 할 때에 왼쪽 화살표를 눌렀을 때(블록이 왼쪽 이동)와 오른쪽 화살표를 눌렀을 때(블록이 오른쪽으로 이동)에 각자 다른 결과물을 주어야 합니다. 이런 경우에 조건문으로 각 상황들을 조율해줍니다.  

### if문
---
**기본 형태**  

```
if(조건){ // 조건이 참일 경우 문장 실행
    // 문장
}
else if(조건){ // 위의 조건이 거짓이고 해당 조건이 참일 경우 문장 실행
    // 문장
}
else if(조건){ // 위의 조건들이 거짓이고 해당 조건이 참일 경우 문장 실행
    // 문장
}
else { // 위의 모든 조건들이 거짓일 경우 문장 실행
    // 문장
}
```

가장 많이 쓰이는 형태의 조건문 입니다. if, else if, else를 이용해서 각 상황별로 조건을 제시합니다. else if와 else는 생략될 수 있으며 이 경우에 if문에서 조건이 참이 아닌 경우 중괄호 안의 코드를 무시합니다.  

```
#include <stdio.h>

int main()
{
    int i=0;

    if(i==1){
        printf("Hello World!");
    }

    return 0;
}
출력 결과:

```

아무것도 출력되지 않는 것을 확인할 수 있습니다. else if는 중간 조건으로 원하는 조건의 개수만큼 올 수 있습니다. 다음은 정수를 한 개 입력받아 양수, 음수, 0 조건에 따라 출력을 해주는 예제입니다.  

```
#include <stdio.h>

int main()
{
    int num;

    printf("정수를 입력하세요 : ");
    scanf("%d",&num);

    if(num<0){
        printf("입력하신 정수는 음수입니다.\n");
    }

    else if(num>0){
        printf("입력하신 정수는 양수입니다.\n");
    }

    else if(num==0){
        printf("입력하신 정수는 0입니다.\n");
    }

    return 0;
}
```

조건문은 처음에 if문의 조건문이 참인지 확인하고 거짓이면 다음 else if문으로, 또 거짓이면 다음 else if문으로 갑니다. 모든 조건에 해당하지 않을 경우 else문의 문장을 아래와 같이 실행시킵니다. 아래의 코드는 위와 같은 결과를 냅니다. num이 0보다 크거나 작지 않다면 else로 가게 되고 이 경우는 num이 0인 경우에 해당됩니다.  

```
#include <stdio.h>

int main()
{
    int num;

    printf("정수를 입력하세요 : ");
    scanf("%d",&num);

    if(num<0){
        printf("입력하신 정수는 음수입니다.\n");
    }

    else if(num>0){
        printf("입력하신 정수는 양수입니다.\n");
    }

    else {
        printf("입력하신 정수는 0입니다.\n");
    }

    return 0;
}
```

조건이 겹칠 경우에는 앞의 조건만 실행시키고 해당 조건문을 빠져나갑니다. 아래의 코드에서 2이상은 출력될 수 없습니다. 2 이상인 숫자를 입력해도 1이상 조건이 먼저 있기 때문에 1이상을 출력하고 해당 조건블록을 빠져나갑니다.  

```
#include <stdio.h>

int main()
{
    int num;

    printf("정수를 입력하세요 : ");
    scanf("%d",&num);

    if(num>=1){
        printf("1이상\n");
    }

    else if(num>=2){
        printf("2이상\n");
    }

    else {
        printf("입력하신 정수는 1보다 작습니다.\n");
    }

    return 0;
}
```

### switch문
---
**기본 형태**  

```
switch(조건문){
    case c1:    // 조건이 참일 경우 여기서부터 아래 문장 전부 실행
        문장;
        break;  // 조건문을 빠져나감
    case c2:
        문장;
        break;
    case c3:
        문장;
        break;
    default:    //위의 조건들에 일치하지 않을 경우 실행
        문장;
        break;
}
```

c1, c2, c3 자리에 변수나 실수, 문자열은 들어갈 수 없습니다. 조건이 참이면 해당 조건문 실행문장만 실행하고 전체 조건문을 빠져나가는 if문에 비해 조건이 참이면 그 조건부터 아래 문장들을 쭈욱 전부 실행시킨다는 차이점이 있습니다. 예를들어 아래의 실행차이가 있습니다.  

```
// if문
#include <stdio.h>

int main()
{
    int num = 1;

    if(num==1){
        printf("1\n");
    }

    else if(num==2){
        printf("2\n");
    }

    else {
        printf("3\n");
    }

    return 0;
}
출력 결과:
1

// switch문
#include <stdio.h>

int main()
{
    int num = 1;

    switch(num){
        case 1 :
            printf("1\n");
        case 2:
            printf("2\n");
        default:
            printf("3\n");
    }

    return 0;
}
출력 결과:
1
2
3
```

그 조건부터 아래 조건들의 실행 문장까지 전부 실행시키는 것이 싫다면 break;로 해당 조건문을 탈출하면 됩니다.  

```
#include <stdio.h>

int main()
{
    int num = 1;

    switch(num){
        case 1 :
            printf("1\n");
            break;
        case 2:
            printf("2\n");
            break;
        default:
            printf("3\n");
            break;
    }

    return 0;
}
출력 결과:
1
```

switch문은 내부를 들여다보면 실제로는 다중 if문과 같이 동작합니다. 따라서 성능적인 이득은 없는 셈입니다. 가독성은 좋으나 성능 향상에는 도움이 되지 않다는 것을 기억해야합니다.

### look-up table 이용하기
---
if문과 switch문은 조건이 많아질수록 겹겹이 사용하게 되면서 성능적인 결함이 생깁니다. 이럴 경우에 look-up table을 사용한다면 훨씬 빠르게 처리할 수 있습니다.  
차이를 느끼기 위해 월을 입력받아서 해당 월에 몇일까지 있는지 알아보는 프로그램을 짜보겠습니다. 윤년은 배제하고 프로그래밍을 했습니다.

```
#include <stdio.h>


int main()
{
    int month = 0;
    int day = 0;

    printf("월을 입력해주세요 : ");
    scanf("%d",&month);

    switch(month){
        case 1:
            day = 31;
            break;
        case 2:
            day = 28;
            break;
        case 3:
            day = 31;
            break;
        case 4:
            day = 30;
            break;
        case 5:
            day = 31;
            break;
        case 6:
            day = 30;
            break;
        case 7:
            day = 31;
            break;
        case 8:
            day = 31;
            break;
        case 9:
            day = 30;
            break;
        case 10:
            day = 31;
            break;
        case 11:
            day = 30;
            break;
        case 12:
            day = 31;
            break;

    }

    printf("%d월에는 %d일까지 있습니다.",month,day);

}
```

이것을 룩업 테이블로 바꾸보겠습니다. 룩업 테이블은 주로 문자열이나 배열을 이용하여 데이터를 구성해놓고 포인터나 인덱스를 이용하여 데이터에 접근하는 방식으로 속도상의 이점이 있어서 자주 사용됩니다.

```
#include <stdio.h>

int searchDay(int m){
    int month[12] = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
    return month[m-1];
}


int main()
{
    int month;
    int day;

    printf("월을 입력해주세요 : ");
    scanf("%d",&month);

    printf("%d월에는 %d일까지 있습니다.",month,searchDay(month));

}
```



### goto문
---
조건 없이 어떤 위치로 점프시켜 줍니다. C언어의 절차지향적인 특성에 어긋나는 문법이므로 많은 프로그래머들이 싫어합니다.  

```
#include <stdio.h>

int main()
{
    int num = 1;

    goto hi;

    printf("실행 안됨\n");

    hi:
        printf("hi~\n");

    return 0;
}
출력 결과:
hi~
```

거의 유일하게 사용되는 경우는 예외처리를 위한 경우입니다.

```
#include <stdio.h>

int main()
{
    int age = 0;

    printf("나이를 입력해주세요 : ");

    scanf("%d",&age);

    if(age<=0)
        goto ERROR;

    printf("나이 출력");

    return 0;

    ERROR:
    printf("나이는 0 이하일수 없습니다.");
    return -1;
}
```

이런식으로 프로그램이 잘못 동작할 경우엔 특정 장소로 이동시켜서 예외를 처리해주는데 가끔 쓰입니다.