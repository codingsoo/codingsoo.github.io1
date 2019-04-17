---
title: C언어 열거형
keywords: C언어 열거형, enum
last_updated: September 17, 2017
tags: [C언어]
summary: "C언어 열거형에 대한 이야기"
sidebar: c_language_sidebar
permalink: C언어-열거형.html
folder: c_language
---

## 열겨형

### 개요
---
열거형(enumeration)이란 변수가 가질 수 있는 값들을 미리 열거해 놓은 자료형입니다. enum은 둘 이상의 연관이 있는 이름을 상수로 선언함으로써 프로그램의 가독성을 높이는데 사용됩니다.  


```
#include <stdio.h>

enum {
    Do=1, Re=2, Mi=3, Fa=4, So=5, La=6, Ti=7
};

int main(int argc, const char * argv[]) {
    printf("%d",Do);
}
결과값 : 1
```
이렇게 숫자에 이름을 붙여줄 수 있는 것입니다. 아래의 예제처럼 구조체 비슷하게 쓸 수도 있습니다.

```
#include <stdio.h>

typedef enum syllable{
    Do=1, Re=2, Mi=3, Fa=4, So=5, La=6, Ti=7
} Syllable;

void Sound(Syllable sy){
    switch(sy){
        case Do:
            fputs("도!",stdout); return;
        case Re:
            fputs("레!",stdout); return;
        case Mi:
            fputs("미!",stdout); return;
        case Fa:
            fputs("파!",stdout); return;
        case So:
            fputs("솔!",stdout); return;
        case La:
            fputs("라!",stdout); return;
        case Ti:
            fputs("시!",stdout); return;
    }
}

int main(int argc, const char * argv[]) {
    Syllable tone;
    for(tone=Do; tone<=Ti; tone+=1)
        Sound(tone);
    return 0;
}

결과값 : 도!레!미!파!솔!라!시!
```
