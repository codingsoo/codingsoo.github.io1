---
title: C언어 구조체
keywords: C언어 구조체
last_updated: September 17, 2017
tags: [C언어]
summary: "C언어 구조체 이야기"
sidebar: c_language_sidebar
permalink: C언어-구조체.html
folder: c_language
---

## 구조체

### 개요
---
구조체는 데이터들을 한데 묶기 위해 사용하는 것입니다. 배열과 달리 서로 다른 자료형도 묶을 수 있습니다.   

```
struct 태그 {
    자료형1 멤버1
    자료형2 멤버2
}; // 구조체의 정의

struct 태그 변수명; // 구조체 변수 선언
```

구조체 변수를 선언한 뒤 사용하고 싶다면 . 연산자를 이용합니다. 변수를 저장할 때에는 중괄호를 이용합니다.  

```
struct student {
    int number;
    char name[10];
    double grade;
};

struct student s1 = { 25, "kms", 3.92 };

s1.number // 25
s1.name // kms
s1.grade // 3.92
```

중괄호를 이용 안하고 직접 멤버변수들에 대입시키는 것도 가능합니다.

```
#include <stdio.h>
#include <string.h>

struct student {
    int number;
    char name[10];
    double grade;
};

int main(void)
{

    struct student s1;

    s1.number = 25;
    strcpy(s1.name,"kms");
    s1.grade = 3.92;

    printf("%d %s %f",s1.number,s1.name,s1.grade);

    return 0;
}
```

### typedef + 구조체
---
typedef는 기존에 존재하는 자료형의 이름에 새 이름을 부여하는 것을 목적으로 하는 선언입니다.

```
typedef int INT; //int의  다른 이름 INT 부여!
typedef int * PTR_INT //int * 의 다른 이름 PTR_INT 부여!
```

위와 같은 방식으로 우리는 이미 있는 자료형을 편하게 쓸 수 있습니다. 특히 구조체와 연결되면 편리하게 사용이 가능합니다.

```
struct point{
  int xpos;
  int ypos;
};
```

위와 같은 구조체를 사용하려면 아래와 같이 구조체 변수를 선언해야 합니다.

```
struct point pos;
```

그런데 다음과 같이 편하게 typedef를 적용해 볼 수 있습니다.

```
struct point{
  int xpos;
  int ypos;
};
typedef struct point Point;
Point pos;
```

위와 같은 방식은 보통 아래 처럼 축약되어 사용됩니다.
그럼 앞으로 간편하게 구조체 변수를 선언할 수 있습니다.

```
typedef struct point{
  int xpos;
  int ypos;
} Point;

Point pos;
```

### 구조체 안의 구조체
---
구조체는 다른 구조체를 멤버변수로 갖을 수 있습니다.  

```
typedef struct point{
  int xpos;
  int ypos;
} Point;

typedef struct square{
    Point p1, p2;
}Square;
```

위의 코드는 두 점을 멤버변수로 갖는 구조체 Square를 설명하기 위한 것입니다. 각 점 Point가 또 구조체입니다.  
p1와 p2의 xpos, ypos에 접근하기 위해서는 .연산자를 두 번 이용합니다.  

```
Square s;
s.p1.xpos = 10;
s.p1.ypos = 20;
s.p2.xpos = 30;
s.p2.ypos = 40;
```

### 구조체 배열
---
구조체도 배열로 나타낼 수 있습니다.

```
typedef struct point{
  int xpos;
  int ypos;
} Point;

Point p[10];

p[0].xpos = 10; // p구조체 배열의 첫번째 원소에 xpos의 값을 10으로 정합니다.
p[0].ypos = 10; // p구조체 배열의 첫번째 원소에 ypos의 값을 10으로 정합니다.
```

### 구조체 포인터
---
```
#include <stdio.h>

typedef struct point{
    int xpos;
    int ypos;
} Point;

void OrgSymTrans(Point * ptr){ 
    ptr -> xpos = (ptr->xpos)* -1;
    ptr -> ypos = (ptr->ypos)* -1;
}

void ShowPosition(Point pos){
    printf("[%d, %d] \n", pos.xpos, pos.ypos);
}

int main(int argc, const char * argv[]) {

    Point pos={7, -5};

    OrgSymTrans(&pos);

    ShowPosition(pos);

    return 0;
}
```

주어진 점을 원점대칭 이동을 시킨 뒤에 보여주는 코드입니다. 포인터로 받는 것은 같고 포인터로 받은 구조체 안의 변수들에 접근할 때에 ptr -> xpos 꼴로 쉽게 접근할 수 있음을 알 수 있습니다.  
구조체를 포인터 형태로 나타내는 이유는 일반 구조체로 나타내면 구조체의 복사본이 함수로 전달되게 됩니다. 만약 구조체의 크기가 크면 그만큼 시간과 메모리가 소요됩니다. 반면에 포인터로 주소값만 넘긴다면 그만큼 시간과 메모리가 절약되는 것이지요. 다만 포인터를 사용한다면 원본 파일이 변경되는 것이니 목적에 맞게 사용하시면 됩니다.
