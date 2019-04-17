---
title: C언어 공용체
keywords: C언어 공용체
last_updated: September 17, 2017
tags: [C언어]
summary: "C언어 공용체 이야기"
sidebar: c_language_sidebar
permalink: C언어-공용체.html
folder: c_language
---

## 공용체

### 개요
---
공용체란 같은 메모리 영역을 여러 변수들이 공유하는 자료형입니다.

```
typedef union point{
    int a;
    char b;
} Point;
```

앞서 본 struct가 union으로 바뀌었을 뿐입니다. 가장 큰 다른점은 struct는 내부 변수가 각각의 주소를 갖지만 union은 그렇지 않다는 것입니다. 공용체는 선언된 변수들 중에 가장 크기가 큰 변수를 기준으로 메모리 공간을 공유합니다. int는 4바이트, char는 1바이트 이므로 char는 따로 메모리 공간을 갖지 않고 int가 차지하는 4바이트 안의 제일 앞 1바이트를 차지하는 것입니다. 저 공용체는 4바이트의 크기를 갖게 되는 것이죠.  

```
typedef union point{
    int a;
    char b;
} Point;


int main(int argc, const char * argv[]) {

    Point po;
    po.a = 4;
    po.b = 5;

    printf("%d",po.a);
    return 0;
}
```

po.a에 4를 저장했지만 출력 결과는 5가 됩니다. b가 a의 1바이트를 차지하므로 po.b가 5로 바뀌면서 po.a의 값도 바뀌게 된 것입니다.  

### 활용 
---
같은 수를 다른 방식으로 관리할 필요성이 있는 경우에 많이 활용됩니다. 네트워크 프로그래밍에 많이 활용됩니다. 

```
#include <stdio.h>

typedef union _IP_ADDR{
    int nAddress;
    short awData[2];
    unsigned char addr[4];
} IP_ADDR;

int main()
{
    IP_ADDR addr;

    addr.addr[0] = 192;
    addr.addr[1] = 164;
    addr.addr[2] = 10;
    addr.addr[3] = 3; // 192.164.10.3 IP 주소 저장

    printf("%d\n",addr.nAddress); // 51029184로 다르게 표현 가능

    return 0;

}
```