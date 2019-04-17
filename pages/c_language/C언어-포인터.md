---
title: C언어 포인터 이야기(심화)
keywords: C언어 포인터
last_updated: September 20, 2017
tags: [C언어]
summary: "C언어 포인터 활용에 대한 이야기"
sidebar: c_language_sidebar
permalink: C언어-포인터.html
folder: c_language
---

## 포인터의 활용

### 간접참조 연산자와 증감연산자
---
- v = *ptr++ => ptr가 가리키는 값을 v에 대입한 후에 ptr를 증가한다.
- v = (*ptr)++ => ptr가 가리키는 값을 v에 대입한 후에 가리키는 값을 증가한다.
- v = *++ptr => ptr를 증가시킨 후에 ptr가 가리키는 값을 v에 대입한다.
- v = ++*ptr => ptr가 가리키는 값을 가져온 후에 그 값을 증가하여 v에 대입한다.

```
#include <stdio.h>

int main()
{
    int i[3] = {10,20,30};

    int *ptr = i;
    printf("%d\n",*ptr++); // *ptr출력후 ptr증가시킴(i[1]로 가리키는값 바뀜)
    printf("%d\n",(*ptr)++); // *ptr출력후 ptr이 가리키는 값 증가시킴(i[1]값이 1증가)
    printf("%d\n",*++ptr); // ptr이 카리키는 값 증가(i[2]로 가리키는값 바뀜)한뒤에 출력
    printf("%d\n",++*ptr); // ptr의 값을 증가시킨 뒤 출력
}
출력 결과:
10
20
30
31
```

### 포인터의 형변환
---
C언어에서는 꼭 필요한 경우에, 명시적으로 포인터의 타입을 변경할 수 있습니다.  

```
double d = 1.123;
double *pd = &d;
int *pi;
pi = (int *)pd;
```

### 참조에 의한 호출
---
포인터 변수는 주소값이 복사되면 간접 참조 연산자인 *를 이용해 해당 변수의 값에 접근할 수 있다는 특징이 있습니다. 그리고 이러한 방식의 함수 호출을 참조에 의한 호출이라고 부릅니다.  
이와 대비되는 개념으로 값에 의한 호출을 먼저 보겠습니다.

```
#include <stdio.h>
void swap(int x, int y);

int main(void) {
    int a = 10, b = 20;
    printf("a=%d b=%d\n", a, b);
    swap(a, b);
    printf("a=%d b=%d\n", a, b);
    return 0;
}

void swap(int x, int y){
    int tmp;

    tmp = x;
    x = y;
    y = tmp;
}
출력 결과:
a=10 b=20
a=10 b=20
```

swap에서 x변수와 y변수의 값을 바꾸어주었습니다. 하지만 원본인 a와 b의 값은 변하고 있지 않습니다. x는 단순히 a의 값을 복사하고 y는 단순히 b의 값을 복사하기 때문에 당연한 일입니다.  
x와 a, y와 b는 완전히 독립적이지요. 이것이 값에 의한 호출 방식입니다. 참조에 의한 호출 방식으로는 외부 변수에 접근이 가능합니다.  

```
#include <stdio.h>
void swap(int *x, int *y);

int main(void) {
    int a = 10, b = 20;
    printf("a=%d b=%d\n", a, b);
    swap(&a, &b);
    printf("a=%d b=%d\n", a, b);
    return 0;
}

void swap(int *x, int *y){
    int tmp;

    tmp = *x;
    *x = *y;
    *y = tmp;
}
출력 결과:
a=10 b=20
a=20 b=10
```
### 이중 포인터
---
이중 포인터(double pointer)란 포인터를 가리키는 포인터를 의미합니다.  

```
int i = 10; 
int *p = &i; 
int **q = &p; // q는 포인터 p를 가리키는 이중 포인터
```

```
#include <stdio.h>
int main(void)
{
    int i = 100;
    int *p = &i;
    int **q = &p;

    printf("%d\n",q); // 포인터 변수 p의 주소값
    printf("%d\n",*q); // i의 주소값
    printf("%d\n",**q); // i의 값
    return 0;
}
```

### 포인터와 const
---
```
#include <stdio.h>

int main(int argc, const char * argv[]) {

    int num = 20;
    const int * ptr = &num;
    *ptr = 30; //에러!
    num = 40; //성공!
}
```

위의 예시에서 const int * ptr = &num; 가 말하는 바는 아래와 같습니다.  
“포인터 변수 ptr을 이용해서 ptr이 가리키는 변수에 저장되는 값을 변경하는 것을 허용하지 않겠습니다!”  
그렇다고 해서 포인터 변수 ptr이 가리키는 변수 num이 상수화되는 것은 아닙니다.  

```
#include <stdio.h>

int main(int argc, const char * argv[]) {

    int num1 = 10;
    int num2 = 20;
    int * const ptr = &num1;
    ptr = &num2; //컴파일 에러!
    *ptr = 40; //컴파일 성공!
}
```
위와 같이 선언을 하면 가리키는 대상을 바꾸는 것은 안되지만 저장된 값을 변경하는 것은 문제가 되지 않습니다.  
const int * const ptr = &num; 이런식으로 선언하는 것도 가능합니다.  

### 포인터 배열과 배열 포인터
---
```
int * a[4]; //포인터 배열
int (*a)[4]; //배열 포인터
```

저 위의 두가지는 어떻게 다를까요?  
  
포인터 배열은 말 그대로 포인터를 담아두는 배열입니다. 아래와 같이 사용하시면 됩니다.  
```
int * a[4] = {&num1, &num2, &num3, &num4};
```

주소값들을 저장하는 포인터 배열이 완성되었지요?  
배열 포인터는 이미 앞서 배열에서 다루긴 했지만 한번 더 보도록 하겠습니다.  

```
#include <stdio.h>

int main(int argc, const char * argv[]) {

    int i = 0, j = 0;
    int arr2d[2][4] = {1,2,3,4,5,6,7,8};

    int (*a)[4] = arr2d;
    for (i=0; i<2; i++) {
        for (j=0; j<4; j++) {
            printf("%d", a[i][j]);
        }
    }
}
```

위처럼 표현하게 되면 a의 포인터가 int형 자료형을 4개씩 건너뜁니다.  
따라서 위의 코드처럼 배열인자로 쓸 수 있게 됩니다.  
3차원의 배열도 한번 해보겠습니다.  

```
#include <stdio.h>

int main(int argc, const char * argv[]) {

    int arr[3][2][2] = {1,2,3,4,5,6,7,8,9,10,11,12};
    int (*a)[2][2] = arr;
    int i=0, j=0, k=0;

    for (i=0; i<3; i++) {
        for (j=0; j<2; j++) {
            for (k=0; k<2; k++) {
                printf("%d ",a[i][j][k]);
            }
        }
    }

}
결과 : 1 2 3 4 5 6 7 8 9 10 11 12
```

### 함수 포인터
---
함수를 포인터로 표현하려면 어떻게 해야할까요?  
아니, 그 전에 함수포인터란 무엇일까요?  
특정 변수에 대한 메모리 주소를 담을 수 있는 변수를 포인터변수라고 합니다.  
함수포인터란, 특정 함수에 대한 메모리 주소를 담을 수 있는 것입니다.  
아래의 코드를 살펴보겠습니다.

```
#include <stdio.h>

void SimpleAdder(int n1, int n2){
    printf("%d + %d = %d \n", n1, n2, n1+n2);
}

void ShowString(char * str){
    printf("%s \n", str);
}

int main(int argc, const char * argv[]) {

    char * str = "hi I'm zerobugplz";
    int num1 = 10, num2 = 20;

    void (*fptr1)(int,int) = SimpleAdder;
    void (*fptr2)(char *) = ShowString;

    fptr1(num1,num2);
    fptr2(str);

    return 0;

}
```

위의 예시에서 SimpleAdder나 ShowString과 같은 함수의 주소값만을 담을 수 있는 것을 볼 수 있습니다.  
  
void (*fptr1)(int,int) = SimpleAdder; 부분으로 설명해 보겠습니다.    
우선 앞부분에는 반환형이 들어갑니다.  
그리고 포인터가 들어가고 그 다음에 인자의 형태만 써주시면 됩니다.  
기존의 함수 원형과 등호표시를 해주시면 해당 함수에 대한 메모리 주소를 받을 수 있습니다.  
위의 코드의 결과값은 아래와 같습니다.

```
10 + 20 = 30
hi I'm zerobugplz
```

함수 포인터는 함수의 배개변수로 전달될 수도 있습니다.  

```
void funcpointer(void(*pf))
{
    pf(); // pf함수 이용 가능
}
```

### 함수 포인터와 룩업 테이블
---
이전에 조건문에서 룩업테이블을 사용하여 더 빠르게 처리했던 것을 생각하면 됩니다. 같은 개념으로 함수를 좀 더 편하게 사용할 수 있고 인덱스와 결합해서 사용할 수 있으므로 반복문이나 의미있는 인덱스와의 결합 등 다양한 활용 방도가 있습니다.

```
#include <stdio.h>

void func1(int num){
    printf("func1 : %d\n",num);
}

void func2(int num){
    printf("func2 : %d\n",num);
}

void func3(int num){
    printf("func3 : %d\n",num);
}

int main(void)
{
    void (*arrfunc[3])(int) = { func1, func2, func3};

    arrfunc[0](1);
    arrfunc[1](10);
    arrfunc[2](100);

    return 0;
}
출력 결과:
func1 : 1
func2 : 10
func3 : 100
```

### volatile 포인터와 void 포인터
---
컴파일러는 최적화를 진행하면서 상당히 많은 양의 코드를 그냥 생략해버립니다. 필요가 없다고 판단되면 생략하는 것이지요. volatile은 다른 프로세스나 스레드가 값을 항상 변경할 수 있으니 값을 사용할 때마다 다시 메모리에서 읽으라는 것을 의미합니다. 즉, volatile으로 선언된 값 관련된 모든 변수들은 생략되지 않고 순서대로 동작합니다.  

```
volatile char *ptr;
```

void 포인터는 순수하게 메모리의 주소만 가지고 있는 포인터입니다.

```
void * ptr; // 선언
```

### 동적할당
---
동적할당에 공부하기 전에 우리가 짜는 코드들이 어디에 저장되는지에 대해서 알아보겠습니다.

- 코드공간 : 프로그램의 코드가 저장됩니다.
- 전역공간 : 전역 변수들이 생성됩니다.
- 스택 : 프로그램이 실행되면서 사용하는 공간으로 주로 함수 호출시에 함수 매개 변수와 함수 안의 지역 변수를 생성하는 공간입니다. 함수 호출 시에 스택에 할당된 공간은 함수 호출이 끝나면 사라지게 됩니다. 따라서 프로그래머는 따로 함수 안에 선언한 변수들을 제거할 필요가 없습니다.
- 힙 : 함수에 일반적으로 변수를 생성하면 제거되지만 동적 할당을 이용한다면 얼마든지 메모리 공간이 허락하는 한 마음대로 사용할 수 있습니다. 프로그래머가 자율적으로 공간을 생성하고 반납해주어야 합니다.  

힙에 동적할당으로 변수를 생성하면 무엇으로 그 변수를 가리켜야 할까요?  
C언어에서는 포인터를 이용하여 그 공간을 가리키도록 합니다.  

```
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int *pi; // 동적 메모리를 가리킬 포인터
    pi = (int*)malloc(sizeof(int)); // 동적 메모리 할당
    *pi = 3; // 동적 메모리 사용
    free(pi); // 동적 메모리 반납
    
    return 0;
}
```

배열은 아래와 같이 나타내어줍니다.

```
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int *pi; // 동적 메모리를 가리킬 포인터
    pi = (int*)malloc(sizeof(int)*4); // 동적 메모리 할당을 받을 때에 int형으로 4칸 받음
    pi[0] = 1; // 동적 메모리 사용
    pi[1] = 2;
    pi[2] = 3;
    pi[3] = 4;
    printf("%d %d %d %d", pi[0], pi[1], pi[2], pi[3]);
    free(pi); // 동적 메모리 반납

    return 0;
}
출력 결과: 1 2 3 4
```

### 메모리 재할당
---
메모리를 190바이트만큼 할당받았다가 200만큼으로 늘리고싶어졌습니다. 이 경우에 사용하는 함수가 재할당 함수 realloc입니다. realloc은 단순히 원래의 메모리를 free시키고 다시 malloc하는 개념이 아닙니다. 아래의 사진과 함께 설명하겠습니다(출처 : 독하게 시작하는 C프로그래밍).  
![realloc](https://zerobugplz.github.io/images/studying/realloc.png)  
메모리를 동적으로 할당받을 때에 힙에서 필요한만큼 잘라서 주게 됩니다. 그러다가 필요없어진 메모리는 다시 반환받지요.  
그런데 이전에 반환받은 200으로 쪼개진 메모리가 있는데 개발자가 다시 190을 달라고한다면? 200짜리를 보통 그냥 줍니다. 190으로 다시 쪼개느니 200짜리를 주는 것이지요. 물론 개발자에게는 190으로 인식됩니다.  
그런데 개발자가 190을 받았는데 200으로 메모리를 늘리고싶어졌습니다. 이 경우에는 시스템이 200짜리를 준 것이 아닌지 한번 체크합니다. 200짜리를 줬을 경우에는 다시 줄 필요없이 200을 쓸 수 있도록 허가만 해주면 되는 것입니다.  
물론 딱 190에 맞게 주었을 경우에는 메모리를 free시킨 뒤에 다시 200만큼 동적할당을 해줍니다.

> realloc(포인터,할당받을 크기)

```
// 12바이트만큼 동적 할당
char * sentence = static_cast<char *>(malloc(sizeof(char) * 12));
// 24바이트만큼 재할당
realloc(sentence,sizeof(char)*24);
```

### 메모리 복사
---
포인터는 정수를 복사하듯이 복사할 수 없습니다. 우선 정수를 복사하는 예제입니다.

```
int a = 10;
int b = a; // b에 a 복사
```

이걸 포인터에서 하면 어떻게 될까요?

```
#include <stdio.h>

int main(void)
{
    int *a = NULL;
    *a = 10;
    int *b = a;
    printf("a : %p, %d\n",a,*a);
    printf("b : %p, %d",b,*b);


    return 0;
}
출력 결과:
a : 0x7fff54105ad8, 10
b : 0x7fff54105ad8, 10
```

값의 복사가 아닌 주소의 복사가 일어나므로 얕은복사(실제 데이터가 복사되는 것이 아닌 참조형태로 복사가 일어나는 것)가 일어납니다. 이렇게 되면 a의 값을 변경하면 b도 따라서 변경되게 되겠지요. b는 단순히 a를 참조하는 변수일 뿐이닌깐요.  
깊은 복사를 해야 데이터가 완전히 복사되고 a와 b는 서로 완벽하게 독립적이게 됩니다. memcpy를 사용하며 동적할당으로 복사할 크기 이상을 갖어야합니다.

> 문법 : memcpy(복사될 주소 포인터,원본 포인터,복사할 크기)


```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main(void)
{
    int number = 10;
    int *a = &number;
    int *b = static_cast<int *>(malloc(sizeof(int))); // 동적할당
    memcpy(b,a,sizeof(*b));
    printf("a : %p, %d\n",a,*a);
    printf("b : %p, %d",b,*b);


    return 0;
}
출력 결과:
a : 0x7fff561faab8, 10
b : 0x7fc5f1c02590, 10
```

### 메모리안의 값 비교
---
memcmp로 메모리 안의 값들을 비교할 수 있습니다. 같다면 0, 다르면 0이 아닌 수가 출력됩니다.

> memcmp(값1의 포인터,값2의 포인터,비교할 바이트 수)

```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main(void)
{
    int data1 = 20;
    int data2 = 20;
    int *ptr1 = &data1;
    int *ptr2 = &data2;

    printf("%d",memcmp(ptr1,ptr2,sizeof(int)));

    return 0;
}
출력 결과 : 0
```

### *와 \&의 차이점
---
둘은 기계어로 보면 아무런 차이도 없지만 *는 그 값을 변경할 수 있는데 반해 \&는 값을 변경할 수 없습니다.
```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main(void)
{
    int data = 10;
    int *ptr = &data;

    printf("%p\n",&data); // &는 *와 마찬가지로 주소값을 알려주지만
    printf("%p",ptr); // *처럼 값을 변경할 수 없습니다.
    
    &data = 20; // 에러
    *ptr = 20; // ptr이 가리키는 값을 20으로 변경

    return 0;
}
```

### 포인터와 최적화
---
포인터는 많이 쓰면 많이 쓸수록 컴파일러가 최적화를 할 때에 프로그램의 복잡도가 증가합니다. 따라서 반드시 포인터를 사용해야 하는 경우인지 고민해보고 사용하시기 바랍니다.  const 를 이용하여 선언하면 복잡도가 상대적으로 낮아지고 가독성이 좋아지므로 const를 사용할수 없는지 항상 고민해보시기 바랍니다. 