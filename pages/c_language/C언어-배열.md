---
title: C언어 배열 이야기
keywords: C언어 배열
last_updated: September 18, 2017
tags: [C언어]
summary: "C언어 배열에 대한 이야기"
sidebar: c_language_sidebar
permalink: C언어-배열.html
folder: c_language
---

## 배열

### 개요
---
배열이란 동일한 타입의 데이터가 여러 개 저장되어 있는 데이터 저장 장소로 각 데이터들은 정수로 접근합니다. 첫번째 인자가 0번째 인덱스와 매칭되며 각 인자마다 -1된 인덱스(배열 원소의 번)와 매칭됩니다. 예를들어 배열 a의 5번째 인자는 a[4]꼴로 접근합니다. 배열을 이용하면 여러개의 값을 하나의 이름으로 저장, 접근, 처리할 수 있습니다.  
아래 예시에서 배열을 사용하는데 사용법은 뒤에서 다룰 것이기 때문에 여기서는 장점은 대충 감만 잡아주시기 바랍니다.  

```
#include <stdio.h>

int main() {

    int student1_score = 10;
    int student2_score = 90;
    int student3_score = 60;

    printf("1번째 학생의 점수 : %d\n", student1_score);
    printf("2번째 학생의 점수 : %d\n", student2_score);
    printf("3번째 학생의 점수 : %d\n", student3_score);

    return 0;
}
출력 결과:
1번째 학생의 점수 : 10
2번째 학생의 점수 : 90
3번째 학생의 점수 : 60
```

이런 식으로 학생들의 점수를 저장할 수도 있습니다. 하지만 배열을 이용한다면 더 간단하게 처리가 가능합니다.  

```
#include <stdio.h>

int main() {

    int student_score[3]; // 우선은 이런식으로 선언하는구나 보기만 해두세요.

    student_score[0] = 10; // 지금은 뭔지 모르셔도 됩니다.
    student_score[1] = 90;
    student_score[2] = 60;

    printf("1번째 학생의 점수 : %d\n", student_score[0]);
    printf("2번째 학생의 점수 : %d\n", student_score[1]);
    printf("3번째 학생의 점수 : %d\n", student_score[2]);

    return 0;
}
출력 결과:
1번째 학생의 점수 : 10
2번째 학생의 점수 : 90
3번째 학생의 점수 : 60
```

학생들의 점수가 student_score로 일관성 있게 관리되므로 훨씬 편합니다. 또한 인덱스가 정수로 이루어져있기 때문에 for문과도 찰떡궁합입니다.

```
#include <stdio.h>

int main() {

    int student_score[3]; // 우선은 이런식으로 선언하는구나 보기만 해두세요. 

    student_score[0] = 10; // 지금은 뭔지 모르셔도 됩니다.
    student_score[1] = 90;
    student_score[2] = 60;

    for(int i=0; i<3; i++)
        printf("%d번째 학생의 점수 : %d\n", i+1, student_score[i]);

    return 0;
}
출력 결과:
1번째 학생의 점수 : 10
2번째 학생의 점수 : 90
3번째 학생의 점수 : 60
```

### 기본 사용법
---
배열은 자료형 배열이름 배열크기 순서대로 정의합니다.  
예를 들어 int student_score[3]; 라고 정의한다면 int 형의 student_score 이름을 갖는 변수가 3개 선언된 것입니다.  
첫 번째의 원소에는 student_score[0], 두 번째의 원소는 student_score[1] 이런식으로 정수형 인덱스로 접근합니다.  
앞서 개요에서 보았듯이 for문과 잘어울리는 이유를 아실 수 있을 것입니다. 인덱스가 연속된 숫자이니 for문에서 인덱스에 접근하기 용이한 것입니다.  
유의하실 점은 int student_score[3]; 으로 선언했다면 student_score[0] ~ student_score[2] 까지 있다는 것입니다. student_score[3]은 존재하지 않습니다.  

### 배열의 초기화
---
배열은 어떤식으로 초기화를 할까요?  

int student_score[3] = {10, 90, 60}; 이런 식으로 선언과 동시에 초기화가 가능합니다.  
중괄호 안의 값들은 인덱스에 순서대로 담깁니다. 혹은 위의 3을 생략할수도 있습니다.  
int student_score[] = {10, 90, 60}; 이런 식으로 배열의 크기가 주어지지 않으면 자동적으로 초기값의 개수만큼이 배열의 크기로 잡히게 됩니다.

```
int student_score[5] = {10, 90, 60};
```

위와 같이 배열의 크기를 5로 하고 초기화를 3개만 해주면 어떻게 될까요?  
3번째 원소까지만 주어진 값으로 초기화가 이루어지고 4번째와 5번째 원소는 0으로 초기화가 됩니다.  

```
int student_score[5];
```

위의 경우에는 모든 원소가 0이 아닌 쓰레기값으로 초기화가 됩니다.  
차이점에 주의하세요!  

### 배열 원소의 개수 구하기
---
해당 배열에 원소가 몇개가 있는지 알수 있는 방법이 있을까요? sizeof 연산자를 이용하면 쉬워집니다.  

```
#include <stdio.h>

int main() {

    int student_score[3];
    int size;

    student_score[0] = 10;
    student_score[1] = 90;
    student_score[2] = 60;

    size = sizeof(student_score)/ sizeof(student_score[0]);

    for(int i=0; i<size; i++)
        printf("%d번째 학생의 점수 : %d\n", i+1, student_score[i]);

    return 0;
}
```

배열 전체의 크기에서 배열 한개가 차지하는 크기를 나누어주면 됩니다.  
왜 귀찮게 3이라고 입력하지 않고 size를 저런식으로 수식으로 표현해주는 것일까요?  
그 이유는 student_score 배열의 크기가 변해도 저런식으로 프로그래밍을 한다면 size를 일일히 변경해 줄 필요가 없기 때문입니다.  

### 배열의 복사
---
배열을 복사하려면 어떻게 해야할까요?

```
#include <stdio.h>

int main() {

    int a_score[5] = {1,2,3,4,5};
    int b_score[5];
    
    b_score = a_score; // 오류

    return 0;
}
```

위처럼 그냥 배열의 이름으로 대입은 안됩니다.  
**배열의 원소를 일일히 복사해주어야합니다.**  

```
#include <stdio.h>

int main() {

    int a_score[5] = {1,2,3,4,5};
    int b_score[5];
    int size = sizeof(a_score)/ sizeof(a_score[0]);

    for(int i=0; i<size; i++)
        b_score[i] = a_score[i];

    return 0;
}
```

### 2차원 배열 선언 및 하기
---
2차원 배열은 단순히 대괄호를 하나 늘리면 됩니다. 예를 들어서 arr[3][4]이런 식으로 써주면 됩니다. 초기화 방식도 1차원 배열과 비슷합니다. 두 가지를 지원합니다.

```
// 초기화 방식 1
char aList[3][4] = {
             {'a','b','c','d'},
             {'e','f','g','h'},
             {'i','j','k','l'}
     };

// 초기화 방식 2
char aList[3][4] = {'a','b','c','d','e','f','g','h','i','j','k','l'};
```

## 배열과 포인터

### 개요
---
배열의 이름은 배열의 시작주소를 가리키는 포인터입니다. 단, 가리키는 주소를 바꿀 수 없는 상수형 포인터입니다. 이러한 특성 때문에 배열은 다양한 특성을 갖습니다.  

### 배열과 포인터의 관계
---
배열의 이름과 인덱스로 배열이 갖는 값들에 접근할 수 있었습니다. 포인터를 이용해도 이러한 일들이 가능합니다.

```
int arr[3] = {11, 22, 33};
int * ptr = arr;
printf("%d %d %d \n",*ptr,*(ptr+1),*(ptr+2));
printf("%d %d %d \n",ptr[0], ptr[1], ptr[2]);
printf("%d %d %d \n",*arr,*(arr+1),*(arr+2));
printf("%d %d %d \n",arr[0], arr[1], arr[2]);
출력 결과:
11 22 33
11 22 33
11 22 33
11 22 33
```

위에서 유의하셔야할점은 arr+1은 arr주소값에 1이 더해지는 것을 의미하는 것이 아닌 4가 더해지고 있다는 것입니다.  
ptr도 마찬가지입니다. 1을 더하는데 4가 증가되는 이유는 포인터에서는 선언된 값을 메모리에 참조값으로 사용합니다.  
위의 경우에 int형 포인터이므로 4바이트 크기의 메모리를 정수의 형태로 참조하게 되는 것입니다. char형을 참조한다면 1을 더하면 1만 증가될 것입니다.  

### 함수의 인자로 배열을 넘기기
---
함수의 인자로 배열이 넘어갈 수 있을까요?  
네, 있습니다. 하지만 여지껏 보았던 자료형과는 약간 다릅니다.  
먼저 여지껏 보았던 자료형이 함수의 인자로 넘어갈 때 일어나는 일을 설명드리겠습니다.  

```
#include <stdio.h>

void Add(int n);

int main() {

    int a = 1;

    Add(a);

    printf("%d",a);

    return 0;
}

void Add(int n)
{
    n = n+1;
}
```

위의 코드에서 Add(a)를 거치면 1이 Add함수에서 더해져서 a의 값도 증가할까요?  
아닙니다. 사실 n은 a와는 완전 별개의 변수이기 때문입니다. 인자를 a로 주긴 했지만 값의 복사만 일어날 뿐이지 n이 a자체를 가리키지는 않습니다. n=a; n에 a의 값의 복사만 일어날 뿐이지요. 이러한 함수 호출 방식을 Call by value라고 부릅니다.  
값에 의한 호출로서 전달받는 변수의 값에 접근할 수 없다는 특징이 있습니다. 단순히 값의 복사만 일어날 뿐이지요.  
일반적인 자료형이 Call by value형태로 호출되는데 반해 배열은 기본적으로 Call by reference 형태로 호출됩니다.  
아래의 Call by reference를 이용하면 전달 받는 변수를 조작할 수 있습니다.  


```
#include <stdio.h>

void SquareArray(int arr[], int size);

int main() {

    int a[3] = {1,2,3};

    SquareArray(a,3);

    for(int i=0; i<3; i++){
        printf("%d \t",a[i]);
    }

    return 0;
}

void SquareArray(int arr[], int size)
{
    for(int i=0; i<size; i++){
        arr[i] = arr[i]*arr[i];
    }
}
출력 결과 : 
1 	4 	9
```

이러한 일이 가능한 이유는 배열은 함수에서 매개변수를 전달받을 때 포인터의 개념으로 전달받기 때문입니다. 포인터, 즉 주소의 값이 복사되므로 SquareArray 함수에서도 주소 값을 이용하여 main 함수의 배열 a에 접근할 수 있게되는 것입니다.  
이러한 호출방식을 Call by reference라고 부릅니다.  

### 다차원 배열과 포인터의 관계
---
다차원 배열은 일차원 배열과 메모리 구조가 완전히 동일합니다.  
arr[2][2]는 arr[4]와 완전히 메모리 구조가 동일합니다. 접근 방식이 다를 뿐!

> arr[2][2] => arr[0][0], arr[0][1], arr[1][0], arr[1][1]
> arr[4] => arr[0], arr[1], arr[2], arr[3]

그리고 다차원 배열은 배열 포인터의 접근방식도 달라집니다. 예시와 함께 설명해보겠습니다.

```
#include <stdio.h>

int main(int argc, const char * argv[]) {

    int arr2d[2][2] = {1,2,3,4};

    printf("%d, %d",arr2d,arr2d[0]);
}
결과값 : 1606416288, 1606416288
```

둘다 같은 값이 나옵니다. 그렇다면 같은 것일까요?  
아래 코드를 하나 더 보겠습니다.  

```
#include <stdio.h>

int main(int argc, const char * argv[]) {

    int arr2d[2][2] = {1,2,3,4};

    printf("%d, %d",sizeof(arr2d),sizeof(arr2d[0]));
}
결과값 : 16, 8
```

자, 왜 사이즈가 다를까요? 우리는 이 결과값으로 다음과 같은 결론을 낼 수 있습니다.  

> arr2d는 첫 번째 요소를 가리키면서 배열 전체를 의미합니다.  
> arr2d[0]은 첫 번째 요소를 가리키면서 배열의 1행만을 의미합니다.  
  
그리고 특징을 아래의 코드로 더 살펴보겠습니다.  

```
#include <stdio.h>

int main(int argc, const char * argv[]) {

    int arr2d[2][2] = {1,2,3,4};

    printf("%d, %d, %d",arr2d, arr2d+1,arr2d[0]+1);
}
결과값 : 1606416288, 1606416296, 1606416292
```

arr2d는 1을 더하면 가리키는 행이 바뀌고 arr2d[0]에는 1을 더하면 가리키는 열이 바뀝니다. 참조하는 값에 따라서 덧셈시 더해지는 값이 다른 포인터의 특성 때문에 일어나는 일입니다.  

### 다차원 배열의 포인터 선언 
---

다차원의 배열을 포인터 변수에 저장하려면 그냥 배열의 이름과 등호를 맺어서는 안됩니다.
```
char aList[2][3][4] = {'a','b','c','d','e','f','g','h','i','j','k','l'};
```
위의 3차원 배열을 가리키는 포인터를 선언해보겠습니다. 우선 aList 포인터를 저장하는 포인터 변수에 대해서 알아보겠습니다.
```
char (*ptr) = aList; // 오류
```
위에서 배웠듯이 aList는 한번에 3*4 즉 12만큼씩 건너뛰어야합니다. 따라 이렇게 써야합니다.
```
char (*ptr)[3][4] = aList;
```
aList[0]와 aList[0][0]등을 저장하는 포인터 변수도 같은 문법으로 건너뛸만큼을 지정해주고 가리킬 포인터를 지정해주시면 됩니다.
```
char (*ptr1)[4] = aList[0];
char (*ptr1)[4] = aList[1];
char (*ptr2) = aList[0][0];
char (*ptr2) = aList[0][1];
char (*ptr2) = aList[0][2];
char (*ptr2) = aList[1][0];
char (*ptr2) = aList[1][1];
char (*ptr2) = aList[1][2];
```