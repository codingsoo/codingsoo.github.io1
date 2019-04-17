---
title: C언어 문자 자료형
keywords: C언어 문자 자료형, char
last_updated: September 15, 2017
tags: [C언어]
summary: "C언어 문자 자료형에 대해 알아봅시다."
sidebar: c_language_sidebar
permalink: C언어-문자자료형.html
folder: c_language
---

## 문자 자료형

### 문자를 표현하는 방법 - 아스키코드
---
보통 C언어에서는 정수 자료형인 char를 이용하여 문자 한개를 저장합니다.  

```
#include <stdio.h>

int main()
{
    char ch1 = 65;
    char ch2 = 'A';

    printf("%c %c %d %d",ch1, ch2, ch1, ch2);

    return 0;
}
출력 결과:
A A 65 65
```

위 처럼 서식문자는 %c를 이용합니다. 그런데 65는 왜 A로 표현되는 것일까요? 또 왜 A는 10진수 서식문자 %d를 이용하면 65로 출력되는 것일까요?  
그 이유는 아스키코드 규칙 때문입니다.  
아스키코드에서 65는 A를 나타내게 합니다. 66은 B, 67은 C 이렇게 1대1로 매핑되어 있는 것입니다. 문자를 표현하기 위해 특정 문자를 숫자에 대응시킨 것을 인코딩이라고 합니다. 그리고 한 나라의 문자를 표로 정리한 것을 코드 페이지라 합니다.  

![아스키코드](https://zerobugplz.github.io/images/studying/ascii.png)  

위의 아스키코드 페이지에서 궁금할 수 있는 점은 한글이 없다는 것입니다. 세계의 문자를 다 담기에는 1바이트는 너무나도 부족합니다. 여러 나라의 문자를 담기에는 그 크기가 작기 때문에 iso10646과 유니코드 컨소시엄이 유니코드를 독자적으로 만들었습니다. 유니코드를 다루는데는 배열의 개념이 필요하므로 배열을 다루면서 다루기로 하겠습니다.

### 0과 '0'은 다르다.
---
'0'은 문자이고 0은 숫자이기 때문에 다릅니다.

```
#include <stdio.h>

int main()
{
    char ch1 = 0;
    char ch2 = '0';

    printf("%c %c %d %d", ch1, ch2, ch1, ch2);

    return 0;
}
출력 결과:
NULL 0 0 48
```

0은 아스키코드에서 NULL입니다. 따라서 숫자 0을 문자로 표현하면 아스키코드 페이지에 의해 NULL이 됩니다. 문자 '0'은 아스키코드에서 48번이기 때문에 10진수로 표현하면 48이 나오는 것입니다.  

### 문자 연산
---
문자는 ASCII 코드 규칙에 따라 정수로 저장되므로 정수처럼 덧셈, 뺄셈 등이 가능합니다.  

```
#include <stdio.h>

int main()
{
    char ch = 'A';

    printf("%c %c", ch, ch+1);

    return 0;
}
출력 결과:
A B
```

A에서 1을 더하면 B가 나오게 됩니다.

### 제어 문자
---
- \n => 줄바꿈을 해줍니다.
- \r => 복귀 줄의 끝에서 시작 위치로 돌아갑니다.
- \t => 수평 탭

```
#include <stdio.h>

int main()
{
    char ch1 = '\n';
    char ch2 = '\r';
    char ch3 = '\t';

    printf("안%c녕%c", ch1, ch1);
    printf("안녕%c김명수", ch2);
    printf("안%c녕", ch3);

    return 0;
}
출력 결과:
안
녕
김명수안	녕
```

출력 결과와 제어문자의 기능을 비교하며 보시면 기능이 쉽게 이해가 갈 것입니다.