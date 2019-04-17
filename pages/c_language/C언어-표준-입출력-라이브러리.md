---
title: C언어 표준 입출력 라이브러리
keywords: C언어 표준 입출력 라이브러리, C언어 표준 파일 입출력 라이브러리
last_updated: September 23, 2017
tags: [C언어]
summary: "C언어 표준 입출력 라이브러리를 알아봅시다."
sidebar: c_language_sidebar
permalink: C언어-표준-입출력-라이브러리.html
folder: c_language
---

## 표준 입출력 라이브러리

### 스트림

우리가 프로그램을 하나 작성했다고 가정합시다. 이 프로그램을 작성하기 위해서는 키보드로 타이핑을 했을 것입니다. 그리고 프로그램을 모니터를 통해 봅니다.  
그런데 생각해보아야 할 것은 프로그램과 키보드, 모니터는 각각 서로 떨어져있는 개체입니다.  
어떻게 이들이 연결될 수 있을까요?  
프로그램상에서 모니터와 키보드를 대상으로 데이터를 입출력 하기 위해서는 이들을 연결시켜 주는 다리가 필요할 것입니다. 이러한 다리의 역할을 하는 매개체를 가리켜 ‘스트림(stream)’이라고 합니다. 기본적인 스트림은 프로그래머가 생성하지 않아도 기본적으로 생성됩니다.  

```
stdin => 표준 입력 스트림으로 키보드와 연결됨
stdout => 표준 출력 스트림으로 모니터와 연결됨
stderr => 표준 에러 스트림으로 모니터와 연결됨
```

스트림은 구체적으로 FILE 구조체를 통하여 구현되어 있고 이는 stdio.h에 정의되어 있습니다.

### printf
---
stdio.h에 들어있는 함수중 하나입니다. 모니터에 출력을 하기 위한 표준 출력 라이브러리 함수입니다. **printf("내용"); 이라고 치면 내용이 화면에 출력됩니다.**  
```
#include <stdio.h>

int main()
{
    printf("안녕하세요~");

    return 0;
}
출력 결과:
안녕하세요~
```
이를 더 유용하고 유연하게 쓰기 위해서 형식 지정자를 사용합니다.  


### 형식 지정자
---
C언어에서는 형식 지정자를 활용하여 입력과 출력시 형식을 지정해줄 수 있습니다.  

```
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    printf("%s\n","Hello, World!");
    printf("%d\n",17);
    printf("%0x\n",17);
    printf("%c",'A');
    return 0;
}
출력 결과:
Hello, World!
Hello, World!
17
11
A
```

위의 결과를 보면 %s를 써주고 뒤에 콤마를 쓰고 "Hello, World!"를 적어도 앞의 "Hello, World!\n"와 같은 효과가 나는 것을 알 수 있습니다. **%s는 문자열을 대체해주는 서식문자**이고 뒤에 오는 Hello, World!를 문자열로 나타내어 준 것입니다. 숫자에서 더 눈에 띄는 활용 방안을 보여드릴 수 있습니다. printf("%d\n",17);와 printf("%0x\n",17); 의 경우 각각 17을 표현하는 것인데 17과 11이 출력됩니다. 그 이유는 **%d는 10진수로 숫자를 표현하는 서식문자**인데 반해 **%0x는 16진수로 숫자를 표현하는 서식문자**이기 때문입니다. **%c는 한 글자를 출력하는 형식 지정자** 입니다. 우리는 이렇게 같은 데이터도 다른 서식문자를 적용함으로써 출력이나 입력값을 달리 할 수 있습니다. 또한 형식 지정자는 아래와 같이 여러개를 사용할 수 있습니다.  

```
#include <stdio.h>

int main()
{
    int age = 25;

    printf("안녕하세요! 제 이름은 %s이고 나이는 %d살 입니다.","김명수",age);

    return 0;
}
출력 결과:
안녕하세요! 제 이름은 김명수이고 나이는 25살 입니다.
```

### scanf
---
우리는 stdio.h 헤더파일에 선언되어있는 **scanf를 사용하여 사용자로부터 입력을 받을 수 있습니다.** scanf("형식 지정자", 변수의 주소값); 을 통해서 사용자로부터 입력을 받을 수 있습니다. 주소값은 변수 앞에 &만 붙여주면 됩니다.
**형식 지정자의 경우 그때 그때 필요한 것을 찾아서 입력하다보면 외워지므로*** 딱히 지금 외울 필요가 없지만 기본적인 것 몇개만 알려드리겠습니다.

- %d(10진수로 입력받음) => int(나중에 배울 정수 자료형을 저장하는 키워드)
- %c(한 글자 입력받음) => char(나중에 배울 문자 자료형을 저장하는 키워드)
- %lf(실수 한개 입력받음) -> double(나중에 배울 실수 자료형을 저장하는 키워드)

형식 지정자와 변수의 자료형은 일치하여야 합니다. 가볍게 숫자를 입력하는 예제를 보여드리겠습니다.

```
#include <stdio.h>

int main()
{
    int num;

    printf("숫자 한 개를 입력해주세요 : ");
    scanf("%d",&num);

    printf("%d\n", num);
    return 0;
}
출력 결과:
숫자 한 개를 입력해주세요 : 
```

"화면에 숫자 한 개를 입력해주세요 :" 가 뜰 것입니다. 저기에 10을 써보도록 하겠습니다. 그럼 화면에 제가 쓴 10이 출력됩니다.  

```
숫자 한 개를 입력해주세요 : 10
10
```

이와 같은 일이 벌어지는 이유는 scanf를 통해서 사용자로부터 입력을 받고 그 값을 num이라는 변수에 저장해 주었기 때문입니다. 여러 개의 입력값을 받을 수도 있습니다.  

```
#include <stdio.h>

int main()
{
    int num;
    char ch;

    printf("숫자와 문자를 한 개씩 입력해주세요 : ");
    scanf("%d %c",&num,&ch);

    printf("%d\n%c\n", num, ch);
    return 0;
}
출력 결과:
숫자와 문자를 한 개씩 입력해주세요 : 10 A    // 10 A 를 입력한 것입니다.
10
A
```

### 문자 단위 입출력 함수  

```
// 문자 단위 출력함수
int putchar(int c);
int fputc(int c, FILE * stream);
-> 함수 호출 성공 시 쓰여진 문자가, 실패 시 EOF반환

// 문자 단위 입력 함수
int getchar(void);
int fgetc(FILE * stream);
-> 파일의 끝에 도달하거나 함수호출 실패 시 EOF 반환
```

차이점은 putchar나 getchar는 stdout, stdin으로 표현되는 표준 입력 스트림으로부터 하나의 문자를 입력받거나 전송하는 함수 입니다.  
그에 반해 fputc나 fgetc는 문자를 전송할 스트림을 지정할 수 있어서 stdout이나 stdin 뿐만 아니라 파일을 대상으로도 데이터를 입력받거나 전송할 수 있습니다.  
  
위에서 EOF를 이야기 하였는데 아래의 예제를 통해서 이것도 살펴보도록 하겠습니다.  

```
#include <stdio.h>

int main(void){
  int ch;

  while(1){
    ch = getchar();
    if(ch==EOF)
      break;
    putchar(ch);
  }
  return 0;
}
```

위와 같이 짜면 계속해서 문자를 하나 입력받으면 바로 그 문자를 리턴해 줍니다. 종료를 하려면 윈도우는 CTRL + Z를, 리눅스는 CTRL + D키를 눌러야 합니다. 이것을 눌러야 EOF가 반환되도록 약속해 놓은 것입니다.  

### 문자열 단위 입출력 함수

흔히 쓰이는 scanf는 공백을 입력받지 못하지만 공백을 입력받는 방법이 있습니다. 아래에서 소개해 드리는 gets 나 fgets를 사용하시면 됩니다. gets는 보안상의 결함으로(크기가 정해져있지 않으므로 다른 메모리 영역에 침입할 수 있는 단점) fgets를 사용하는 것이 더 좋습니다.  

```
// 문자열 출력 함수
int puts(const char * s);
int fputs(const char * s, FILE * stream);
-> 성공 시 음수가 아닌 값을, 실패 시 EOF 반환

// 문자열 입력함수
char * gets(char *s);
char * fgets(char * s, int n, FILE * stream);
파일의 끝에 도달하거나 함수호출 실패 시 NULL 포인터 반환
```

문자열 출력함수의 사용 예시입니다.

```
#include <stdio.h>

int main(int argc, const char * argv[]) {

    char * str = "Simple String";

    printf("hi \n");
    puts(str);
    puts("-----------");
    fputs(str,stdout);printf("\n");
    fputs("hi~",stdout);printf("\n");

    return 0;
}
결과값
hi
Simple String
-----------
Simple String
hi~
```


문자열 입력함수의 사용 예시입니다.

```
#include <stdio.h>

int main(int argc, const char * argv[]) {

    char str[7];
    int i;

    for(i=0; i<3; i++){
        fgets(str,sizeof(str), stdin);
        printf("Read %d : %s \n",i+1,str);
    }
    return 0;
}
My name is myeongsoo라고 입력했을 때의 결과입니다.

Read 1 : My nam
Read 2 : e is m
Read 3 : yeongs
```

공백을 신경쓰지 않고 ‘\0’를 포함해 7글자를 읽습니다. 엔터키까지도 입력으로 받아들이니 주의하셔야합니다.

### 표준 입출력과 버퍼

앞서 우리가 공부한 것들이 ANSI C의 표준에서 정의된 ‘표준 입출력 함수’입니다.  
이러한 표준 입출력 함수를 통해서 데이터를 입출력하는 경우, 해당 데이터들은 운영체제가 제공하는 ‘메모리 버퍼’를 중간에 통과하게 됩니다. 여기서 말하는 메모리 버퍼는 데이터를 임시로 모아두는 곳인데요! 즉, 우리가 키보드를 통해 입력하면 입력버퍼에 우선 저장되는 것입니다.  
키보드로부터 입력된 데이터가 입력 스트림을 거쳐서 입력 버퍼로 들어가는 시점은 엔터키가 눌리는 시점입니다.  
그렇다면 데이터를 목적지로 바로 전송하지 않고 중간에 입출력 버퍼를 두는 이유는 무엇일까요?  
데이터 전송의 효율성 때문입니다. 바로바로 이동시키는 것보다 메모리 버퍼를 둬서 데이터를 한데 묶어서 이동시키는 것이 효율이 좋고 빠릅니다.  
버퍼는 FILE 구조체에 의해 관리됩니다.

```
#include <stdio.h>

int main()
{
    // stdin은 콘솔을 추상화한 표준 버퍼
    FILE * buffer = stdin;

    getchar();
    getchar();
    getchar();
    getchar();

    return 0;
}
```

buffer 메모리를 디버깅하면서 보면 우리가 적은 문자 4개가 buffer로 들어가는 것을 볼 수 있습니다.

### 입출력 관련 보안 결함 이슈

scanf나 gets같은 경우에는 주어진 변수의 사이즈에 관계없이 우선 글자를 다 읽어들입니다.  
이는 우리가 의도하지 않은 주소값으로 데이터가 전달될 수 있음을 의미하므로 심각한 보안 결함입니다. 아래의 코드는 문자가 10개가 훨씬 넘음에도 불구하고 정상 작동합니다.
```
#include <stdio.h>

int main(){

    char arr[10];

    scanf("%s",arr); // qqqqqqqqqqqqqqqqqqq 입력

    return 0;
}
```
따라서 윈도우라면 scanf_s와 같은 개량된 함수를 쓰던가 아니면 저는 자신만의 함수를 만드는 것을 추천드립니다. 예를 들어서 엔터를 칠 때까지 문자를 입력받는 함수를 만들어보겠습니다.

```
#include <stdio.h>

int read_line(char arr[], int limit);

int main(){

    char arr[10];

    int num = read_line(arr,sizeof(arr)); // qqqqqqqqqqqqqqqqqqq 입력

    printf("%s : %d",arr,num); // qqqqqqqqq : 9 

    return 0;
}

int read_line(char arr[], int limit){
    int ch, i=0;

    while((ch=getchar()) != '\n'){
        if(i < limit){
            arr[i] = ch;
            i++;
        }
    }

    arr[i-1] = '\0'; // 문자열의 마지막에는 널값이 들어가야함

    return i-1; // 마지막에는 널값이 들어가므로 실제 문자의 길이는 -1을 해줘야함
}
```

이런 식으로 사용자로부터 입력을 받을 경우에는 꼭 우리가 지정한 범위를 벗어나지는 않았는지 체크를 해줘야합니다.

## 파일 입출력 라이브러리

### 파일의 개념

C에서의 파일은 크게 두가지 종류가 있습니다.

- 텍스트파일 : 텍스트파일은 사람이 읽을 수 있는 텍스트가 들어있는 파일입니다.
- 이진파일 : 사람은 읽을 수 없으나 기계는 읽을 수 있는 파일로 텍스트 파일과는 달리 라인들로 분리되지 않습니다. 모든 데이터들은 문자열로 변환되지 않고 입출력됩니다.

파일을 처리할 때에는 아래의 순서를 지켜야합니다.  

```
파일 열기 => 파일 읽기와 쓰기 => 파일 닫기
```

### 파일 입출력하기(FILE 포인터, fputc, fgetc, fputs, fgets)

FILE 구조체의 포인터를 선언해서 우리는 파일을 열 수 있습니다.

```
FILE * fopen( const char *, const char * );
첫번째 인자 : 처리할 파일 명
두번째 인자 : 파일 처리 종류 지정 (모드)

예) FILE * fp = fopen("data.txt", "rt")
```

파일 처리 모드의 종류는 다음과 같이 있습니다.

- r = 읽기 모드 / 파일이 없을 경우 에러 발생
- w = 쓰기 모드 / 파일이 없을 경우 새로 만들고 파일이 존재하면 내용을 삭제하고 처음부터 기록
- a = 추가 쓰기 모드 / 파일이 없을 경우 새로 만들고 파일이 존재하면 뒤에부터 이어서 기록

fp변수를 활용해서 그냥 파일을 입출력을 할수도 있습니다.

```
int fputc(int c, FILE * stream); //문자 출력
int fgetc(FILE * stream); //문자 입력
int fputs(const char * s, FILE * stream); //문자열 출력
char * fgets(char * s, int n, FILE * stream); //문자열 입력
```

다음은 파일을 생성해서 문자열을 저장하는 예제입니다.

```
#include <stdio.h>

int main(int argc, const char * argv[]) {
    FILE * fp = fopen("input.txt","wb");
    if(fp==NULL){
        puts("파일오픈 실패!");
        return -1;
    }

    fputc('A', fp);
    fputc('B', fp);
    fputs("My name is Hong \n", fp);
    fputs("Your name is Yoon \n", fp);
    fclose(fp);

    return 0;
}
```

이렇게 하면 다음의 텍스트파일이 생깁니다.

```
ABMy name is Hong
Your name is Yoon
```

이번에는 텍스트파일을 불러와서 출력하는 코드를 예제를 보겠습니다.

```
#include <stdio.h>

int main(int argc, const char * argv[]) {
    char str[30];
    int ch;
    FILE * fp=fopen("input.txt","rt");

    if(fp==NULL){
        puts("파일 오픈 실패!");
        return -1;
    }

    ch = fgetc(fp);
    printf("%c \n", ch);
    ch = fgetc(fp);
    printf("%c \n", ch);

    fgets(str, sizeof(str),fp);
    printf("%s", str);

    fgets(str, sizeof(str),fp);
    printf("%s", str);

    fclose(fp);

    return 0;
}
출력 결과:
A
B
My name is Hong
Your name is Yoon
```

### 파일 복사하기(feof)

파일을 복사하려면 파일의 끝을 확인해야 할 것입니다.

```
int feof(FILE * stream);
-> 파일의 끝에 도달한 경우 0이 아닌 값 반환
```

더 이상 읽을 데이터가 존재하지 않으면 0이 아닌 값을 반환합니다. 파일 복사와 같이 파일의 끝을 확인해야 하는 경우에 유용하게 사용됩니다. 참고로 EOF의 경우에는 무조건 파일의 끝에 도달했다고 반환되는 것이 아니라 오류가 난 경우에도 반환이 되니 이것으로 파일의 끝에 도달했는지를 확인할 수는 없습니다.  

```
#include <stdio.h>

int main(int argc, const char * argv[]) {
    FILE * input=fopen("input.txt", "rt");
    FILE * des=fopen("dst.txt","rt");
    int ch;

    if(input==NULL || des==NULL){
        puts("파일오픈 실패!");
        return -1;
    }

    while((ch=fgetc(input))!=EOF)
        fputc(ch, des);

    if(feof(input)!=0)
        puts("파일복사 완료!");

    else
        puts("파일복사 실패!");

    fclose(input);
    fclose(des);

    return 0;
}
```

### 바이너리 파일 입출력(fread, fwrite)

바이너리 파일이란 텍스트 파일을 제외하면 나머지는 다 바이너리 파일이라고 보셔도 됩니다. 숫자로 된 파일이지요(사진같은 것도 알고보면 숫자로 이루어진 바이너리 파일입니다). 바이너리 파일은 텍프트 파일보다 입출력이 훨씬 간단합니다.  

```
int buf[12];
fread((void*)buf,sizeof(int),12,fp); //fp는 FILE 구조체 포인터
-> sizeof(int) 크기의 데이터 12개를 fp로부터 읽어들여서 배열 buf에 저장해라!

int buf[7] = {1, 2, 3, 4, 5, 6, 7};
fwrite((void*)buf, sizeof(int), 7, fp);
-> sizeof(int)크기의 데이터7개를 buf로부터 읽어서 fp에 저장해라!
```

자 그럼 이 두 함수를 이용해서 바이너리 파일을 복사하는 프로그램의 예제를 보겠습니다.  

```
#include <stdio.h>

int main(int argc, const char * argv[]) {
    FILE * src=fopen("profile.jpeg", "rb");
    FILE * des=fopen("pro.jpeg","wb");
    char buf[1000];
    int readCnt;

    if(src==NULL || des==NULL){
        puts("파일오픈 실패!");
        return -1;
    }

    while(1){
        readCnt = fread((void*)buf, 1, sizeof(buf), src);

        if(readCnt<sizeof(buf)){
            if(feof(src)!=0){
                fwrite((void*)buf,1,readCnt,des);
                puts("파일복사 완료");
                break;
            }
            else
                puts("파일복사 실패");

            break;
        }

        fwrite((void*)buf, 1, sizeof(buf), des);
    }

    fclose(src);
    fclose(des);
    return 0;
}
```
우선 readCnt = fread((void)buf, 1, sizeof(buf), src); 구문을 통해서 src로부터 파일을 1sizeof(buf) 만큼 buf로 읽어들입니다.  
if(readCnt<sizeof(buf)) 안에서는 buf사이즈보다 fread함수가 작은 값을 반환했을때 오류가 발생했거나 파일의 끝에 도달할 상태일 것입니다.  
if(feof(src)!=0)를 통해서 오류인지 파일의 끝에 도착한 것인지 체크해줍니다. 그리고 위에서 배열 buf에 저장해 놓은 데이터를 그대로 des에 저장합니다.  
이걸 계속해서 반복하면? 파일이 전부 복사됩니다. 사진같은걸로 시도 해보세요!  

### 텍스트와 바이너리 파일을 동시에 입출력하기(fscanf, fprintf)

fprintf와 fscanf를 사용하면 쉽게 텍스트와 바이너리 파일을 동시에 입출력 할 수 있습니다. 기존의 printf와 scanf랑 사용법이 비슷하므로 사용법 설명은 넘어가겠습니다.  
아래의 예제는 텍스트 데이터인 이름과 성별, 그리고 바이너리 데이터인 나이 정보를 하나의 파일에 저장하는 것입니다.  

```
#include <stdio.h>

int main(int argc, const char * argv[]) {
    char name[10];
    char sex;
    int age;

    FILE * fp = fopen("friend.txt", "wt");
    int i;

    for(i=0; i<3; i++){
        printf("이름 성별 나이 순 입력: ");
        scanf("%s %c %d", name, &sex, &age);
        getchar(); //scanf함수는 엔터 키의 입력을 읽지 않고 버퍼에 남겨두므로 엔터 키의 소멸을 위한 코드
        fprintf(fp, "%s %c %d", name, sex, age);
    }
    fclose(fp);
    return 0;
}
```
그리고 아래의 예제는 위의 파일을 읽어들이는 예제입니다.

```
#include <stdio.h>

int main(int argc, const char * argv[]) {
    char name[10];
    char sex;
    int age;

    FILE * fp = fopen("friend.txt", "wt");
    int ret;

    while(1){

        ret = fscanf(fp, "%s %c %d", name, &sex, &age);
        if(ret==EOF)
            break;
        printf( "%s %c %d", name, sex, age);
    }
    fclose(fp);
    return 0;
}
```

그렇다면 텍스트와 바이너리 데이터가 둘 다 있는 구조체 변수의 경우에는 어떻게 입출력을 할까요?  
구조체 변수를 하나의 바이너리 데이터로 인식하고 처리하면 됩니다.  

```
#include <stdio.h>
typedef struct fren{
    char name[10];
    char sex;
    int age;
} Friend;

int main(int argc, const char * argv[]) {
    FILE * fp;

    Friend myfren1;
    Friend myfren2;

    //파일 입력하기
    fp = fopen("friend.bin","wb");
    printf("이름, 성별, 나이 순 입력: ");
    scanf("%s %c %d", myfren1.name, &(myfren1.sex), &(myfren1.age));
    fwrite((void*)&myfren1, sizeof(myfren1),1,fp);
    fclose(fp);

    //파일 출력하기
    fp=fopen("friend.bin","rb");
    fread((void*)&myfren2, sizeof(myfren2),1,fp);
    printf("%s %c %d \n", myfren2.name, myfren2.sex, myfren2.age);
    fclose(fp);

    return 0;
}
```

### 파일 위치 지시자

경우에 따라서는 파일의 중간 또는 마지막 부분에 저장된 데이터의 일부를 읽어야 하는 경우도 있을 것입니다. 이럴 경우 파일 위치 지시자를 통해서 이동시킬 수 있습니다.  

![fseek](https://zerobugplz.github.io/fseek.png)  

기본적인 사용법은 int fseek(FILE * stream, 이동거리, 시작위치); 입니다.  
위의 그림에서 보듯이 이동거리에 양수가 들어가면 파일의 끝쪽으로 x칸 이동하고 음수가 들어가면 파일의 앞쪽으로 x칸 이동합니다.  
그리고 시작 위치에 SEEK_SET이 들어가면 파일의 맨 앞부터 이동하고 SEEK_CUR이면 현재 위치, SEEK_END이면 파일의 끝부터 이동을 시작합니다.  
다음은 예제입니다.  

```
#include <stdio.h>

int main(int argc, const char * argv[]) {
    FILE * fp = fopen("text.txt", "wt");
    fputs("123456789",fp);
    fclose(fp);

    fp=fopen("text.txt","rt");

    fseek(fp,-2,SEEK_END);
    putchar(fgetc(fp));

    fseek(fp, 2, SEEK_SET);
    putchar(fgetc(fp));

    fseek(fp, 2, SEEK_CUR);
    putchar(fgetc(fp));

    fclose(fp);

    return 0;
}
결과 : 836
```

맨 처음 파일의 끝(EOF)에서 -2칸 이동해서 8이 출력됩니다. 그리고 맨 앞에서(1) 2칸을 이동해서 3이 출력됩니다. 3이 출력되면서 4를 가리키게 되고 거기서 2칸을 더 이동해서 6이 출력됩니다. 그렇다면 파일 위치 지시자의 위치 정보를 알려주는 함수도 있을까요?  
ftell이라는 함수가 있습니다.  

```
long ftell(FILE * stream);
-> 첫번째 바이트를 가리키면 0출력 세번째 바이트를 가리키면 2출력
```

이 ftell이라는 함수는 다음과 같이 파일 위치 지시자의 정보를 임시로 저장할 때에 유용하게 사용됩니다.  

```
#include <stdio.h>

int main(int argc, const char * argv[]) {
    long fpos;
    int i;

    FILE * fp=fopen("text.txt", "wt");
    fputs("1234-",fp);
    fclose(fp);

    fp=fopen("text.txt","rt");

    for(i=0; i<4; i++){
        putchar(fgetc(fp));
        fpos = ftell(fp);
        fseek(fp, -1, SEEK_END);
        putchar(fgetc(fp));
        fseek(fp, fpos, SEEK_SET);
    }
    fclose(fp);

    return 0;
}
결과 : 1-2-3-4-
```

코드를 조금 설명해 드리자면 파일 위치 지시자의 정보를 fpos에 저장하고 있는 것입니다. 이로써 파일 위치 지시자를 어디로 이동시키건 다시 이전 위치로 되돌릴 수 있게 됩니다.  