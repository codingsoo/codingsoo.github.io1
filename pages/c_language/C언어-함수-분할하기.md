---
title: C언어 함수의 분할하는 방법
keywords: C언어 함수
last_updated: September 19, 2017
tags: [C언어]
summary: "C언어 함수를 분할하는 방법입니다."
sidebar: c_language_sidebar
permalink: C언어-함수-분할하기.html
folder: c_language
---

## 함수 분할하기

### 필요성
---
함수를 분할하는 것은 유지보수에 효과적입니다. 같은 기능을 하는 100줄짜리 함수와 50줄짜리 함수 2개가 있다고 가정하고 오류가 났다고 가정하겟습니다. 100줄짜리를 훑는 것보다 함수 2개중에 1개에서 오류가 났을 테니 50줄만 확인하고 오류를 고치는 편이 당연히 시간이 덜 걸릴것입니다.

### 함수 분할 방법
---
분할을 할 때에는 우선 UI와 기능을 나눕니다. 유저에게 보여지는 화면인 UI와 기능 구현 코드는 쉽게 완전히 분리가 가능합니다. 그리고 코드는 가장 작은 기능단위로 여러개의 함수로 쪼개서 만들면 됩니다. 함수가 너무 많아지면 어쩌지? 라는 고민은 할 필요가 없습니다. 여러개의 함수가 합해져서 한 개의 큰 함수를 만들게 하는 것이 이상적입니다.

```
계산기 함수
```

계산기 함수를 main에 다 때려 박는 것 보다 아래와 같이 분할하는 것이 좋습니다.

```
계산기 UI 함수
덧셈 계산 함수
뺄셈 계산 함수
곱셈 계산 함수
나눗셈 계산 함수
계산기 함수(덧셈, 뺄셈, 곱셈, 나눗셈 계산 함수 호출)
```

아래는 분할 예시입니다.

```
#include <stdio.h>

void userinput_UI_Calculator()
{
    printf("안녕하세요. zerobugplz의 계산기입니다.\n");
    printf("제공되는 기능들--------------------\n");
    printf("1. 덧셈 : 숫자+숫자\n");
    printf("2. 뺄셈 : 숫자-숫자\n");
    printf("3. 곱셈 : 숫자*숫자\n");
    printf("4. 나눗셈 : 숫자/숫자\n");
    printf("원하는 번호와 숫자 두 개를 입력해주세요 : ");
}

void useroutput_UI_Calculator(int num){
    printf("계산 결과는 %d 입니다.", num);
}

int add_Calculator(int num1, int num2){
    return num1 + num2;
}

int subtract_Calculator(int num1, int num2){
    return num1 - num2;
}

int multiply_Calculator(int num1, int num2){
    return num1 * num2;
}

int devide_Calculator(int num1, int num2){
    return num1 / num2;
}

int calculator(int cal_option, int num1, int num2){
    if(cal_option==1)
        return add_Calculator(num1, num2);
    else if(cal_option==2)
        return subtract_Calculator(num1, num2);
    else if(cal_option==3)
        return multiply_Calculator(num1, num2);
    else if(cal_option==4)
        return devide_Calculator(num1, num2);
    else{
        printf("없는 계산 옵션입니다. 1~4까지의 정수를 입력해주세요.");
        return -1;
    }
}

int main()
{
    int option, num1, num2, output;

    userinput_UI_Calculator();

    scanf("%d %d %d", &option, &num1, &num2);

    output = calculator(option, num1, num2);
    useroutput_UI_Calculator(output);

    return 0;
}
```