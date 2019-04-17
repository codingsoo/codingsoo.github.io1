---
title: C언어 문자열
keywords: C언어 문자열
last_updated: September 24, 2017
tags: [C언어]
summary: "C언어 문자열에 대한 이야기"
sidebar: c_language_sidebar
permalink: C언어-문자열.html
folder: c_language
---

## 문자열 개념

### 문자를 표현하는 방법
---
지난번에 문자에 대해서 이야기를 했지만 한번 더 다루어보겠습니다. 컴퓨터에서는 각각의 문자에 숫자코드를 붙여서 표시합니다.  
기본적으로는 아스키코드(ASCII code)가 지원됩니다. 0에서 127까지의 숫자를 이용하여 문자를 표현하는 방식인데 세계의 문자를 모두 담기에는 턱없이 부족했습니다.  
그래서 나온 것이 표준적인 16비트 문자코드인 유니코드입니다. 전세계의 모든 문자를 일관되게 표현하고 다룰 수 있도록 설계되어 있습니다.

### 문자열을 표현하는 방법
---
문자열이란 문자들이 여러개 모인 것입니다. 따라서 문자 배열이 곧 문자열이 되는 것입니다. "hi~" 이런식으로 큰 따옴표와 함께 쓰입니다.  
  
C언어에서는 문자열을 처리할때 맨 마지막에 null(\0)을 넣어서 문자의 끝을 명시적으로 표현해줍니다. 우리가 처리하는건 아니고 자동으로 이렇게 처리됩니다.  
아래의 코드를 보시면 쉽게 이해가 가실겁니다. 문자열을 출력할 때에는 %s 서식문자를 이용합니다.

```
#include <stdio.h>

int main(int argc, const char * argv[]) {

    char str[] = "Good morning!";

    printf("배열 str의 크기: %d \n", sizeof(str));
    printf("널 문자 문자형 출력: %c \n", str[13]);
    printf("널 문자 문자형 출력: %d \n", str[13]);

    str[10] = '!'; //요렇게 문자를 바꿔줄수도 있습니다.
    printf("문자열 출력: %s \n", str);
    return 0;
}
출력 결과:
배열 str의 크기: 14
널 문자 문자형 출력: 
널 문자 문자형 출력: 0
문자열 출력: Good morni!g!
```

혹은 우리가 일일히 문자를 각 배열 원소에 대입시켜줄 수도 있습니다. 이 경우에는 명시적으로 꼭 맨 마지막에 문장의 종료를 알리는 NULL문자를 넣어야 합니다.  

```
#include <stdio.h>
int main(void)
{
    char str[6];

    str[0]='H';
    str[1]='e';
    str[2]='l';
    str[3]='l';
    str[4]='o';
    str[5]='\0';

    printf("%s\n",str); 
    return 0;
}
출력 결과:
Hello
```

아래같이 편리하게 선언할수도 있습니다.

```
char str1[] = "hello";
char *str2 = "hello";
```

단, str2의 경우 문자배열이 아니므로 수정할수가 없습니다. 다음은 많이 쓰이는 문자열 관련 함수들입니다.

```
strcpy - 문자열복사
strlen - 문자열의 길이
strcat - 문자열 합치기
strcmp - 문자열 비교
```

### 문자열 상수
---
- 문자열 상수: “HelloWorld”와 같이 프로그램 소스 안에 포함된 문자열 상수
- 문자열 상수는 메모리 영역 중에서 텍스트 세그먼트(text segment) 에 저장
- 텍스트 세그먼트는 값을 읽기만 하고 수정할수는 없는 메모리 영역(이부분은 나중에 자료구조에서 자세히 다루겠습니다)
- 이와 반대되는 개념으로 데이터 세그먼트가 있음

문자열을 텍스트 세그먼트에 저장하고 불러오기만 할 수 있도록 할수도 있습니다. 문자 배열과 다르게 한번 선언하면 문자를 개별로 수정할 수 없습니다. 주로 포인터와 함께 쓰입니다.

```
#include <stdio.h>
int main(void)
{
    char *str = "Hello"; // Hello 가 문자열 상수입니다

    printf("%s\n",str);
    return 0;
}
출력 결과:
Hello
```

아래는 값을 변경하려 했으므로 오류가 나는 코드입니다.  

```
#include <stdio.h>
int main(void)
{
    char *str = "Hello";

    str[0] = 'K';

    printf("%s\n",str);
    return 0;
}
// 오류!
```

## 문자열 다루기

### 문자열 길이 구하기 
---

> strlen(문자열)은 문자의 길이를 리턴해줍니다.

```
#include <stdio.h>
#include <string.h>

int main(){

    char str[] ="hi my name is kms";

    printf("%d",strlen(str)); // 17

    return 0;
}
```

### 문자열 이어붙이기 
---

> strcat(문자열1,문자열2)

문자1과 문자2를 이어붙일 수 있습니다.

```
#include <stdio.h>
#include <string.h>

int main(){

    char greet1[] = "hi~ ";
    char greet2[] = "how are you?";

    printf("%s",strcat(greet1,greet2));

    return 0;
}
출력 결과: hi~ how are you?
```

### 문자열 비교
---

> strcmp(문자열1,문자열2) 

문자열1과 문자열2가 같으면 0을, 같지 않으면 0이 아닌 수를 리턴합니다.

```
#include <stdio.h>
#include <string.h>

int main(){

    char same1[] = "hi~ ";
    char same2[] = "hi~ ";
    char dif[] = "how are you?";

    printf("%d\n",strcmp(same1,same2)); // 0
    printf("%d\n",strcmp(same1,dif)); // -6

    return 0;
}
```

### 문자열 복사 - strcpy와 strdup를 사용해보자 
---

> strcpy(배열,원본)

배열에 원본의 문자열을 복사해줍니다.

```
#include <stdio.h>
#include <string.h>

int main(){

    char arr[100];
    char str[] = "hi hello~";

    strcpy(arr,str);

    printf("%s\n",arr); // hi hello~

    return 0;
}
```

> strdup(포인터,원본)

동적 할당을 해서 포인터로 주소를 가리켜줍니다. strcpy처럼 정식 지원은 아니지만 대부분의 컴파일러가 지원합니다.strcpy와 무슨 차이가 있는지 예시를 보여주겟습니다.  
  
여러개의 문자를 저장하는 변수를 만들어보겠습니다.  

```
#include<stdio.h>

#defineBUFFER_SIZE 100

intmain(){

char * words[100];
char buffer[BUFFER_SIZE];
int n=0; // numberofstrings
// EOF는파일의끝을의미
while(n<4 && scanf("%s",buffer)!=EOF){
    words[n]=buffer;
    n++;
}

for(int i=0; i<4; i++)
    printf("%s\n",words[i]);

return 0;
}
결과:
a, b, c, d를 차례로 입력했을 때
d
d
d
d
```

d만 나오는 이유를 아시겠나요? Words[n]이 buffer를 가리키게 됩니다(단어 값이 아닌 주소값이 복사되므로). Words[0]~words[3]이 다 buffer를 가리키게 되고 buffer는 계속해서 입력받고 지워지고를 반복하다가 가장 마지막에 입력된 데이터만 저장되어있기 때문에 마지막에 입력한 d만 출력이 되는 것입니다.  
그렇다면 문자열을 복사해주는 함수인 strcpy를 사용하면 복사가 되어서 정상적으로 a, b, c, d가 출력이 될까요? 아래의 예제로 살펴보겠습니다.

```
#include <stdio.h>
#include <string.h>

#define BUFFER_SIZE 100

int main(){

char *words[100];
char buffer[BUFFER_SIZE];
int n=0;//numberofstrings
//EOF는파일의끝을의미
while(n<4 && scanf("%s",buffer)!=EOF){
    words[n] = strcpy(words[n],buffer);
    n++;
}

for(int i=0; i<4; i++)
    printf("%s\n", words[i]);

return 0;
}
```

오류가 납니다. strcpy의 첫번째 인자인 words[n]은 포인터 변수일 뿐이지 문자배열이 아니기 때문입니다.  
이럴때 사용하는 것이 strdup입니다. 사용이 종료되면 반드시 free로 메모리 할당을 해제해줘야 합니다.

```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

#define BUFFER_SIZE 100

int main(){

    char *words[100];
    char buffer[BUFFER_SIZE];


    int n=0; //numberofstrings
    //EOF는파일의끝을의미
    while(n<4 && scanf("%s",buffer)!=EOF){
        words[n] = strdup(buffer);
        n++;
    }

    for(int i=0; i<4; i++){
        printf("%s\n",words[i]);
        free(words[i]);
    }

    return 0;
}
```

엄밀히 말하자면 c언어 표준함수는 아니지만 대부분의 컴파일러가 지원합니다. strdup는 문자열을 읽어서 복사본을 반환합니다.  
strdup는 아래처럼 생겻을 것입니다.

```
char *strdup(char*s){
    char *p;
    p = (char*)malloc(strlen(s)+1);
    
    if(p!=NULL)
        strcpy(p,s);
        
    return p;
}
```

### 문자열 검색

strstr함수를 이용해 문자열을 검색할 수 있습니다. 문자열을 검색한 뒤 주소값을 반환합니다. 찾지 못한다면 NULL을 반환합니다.

> strstr(검색 대상,검색할 것)

```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main(void)
{
    char sentence[12] = {"I am a boy."};
    
    // strstr로 am의 시작 주소를 리턴받아서 저장합니다.
    char *psfind = strstr(sentence,"am");
    
    // 시작주소인 sentence를 빼주면 sentence배열의 인덱스가 됩니다.
    int index = psfind - sentence;

    printf("%d",index); // 2

    return 0;
}
```

### 문자열 토크나이징
---
(부경 대학교 권오흠 교수님의 인강을 듣고 작성하는 포스팅)  
우선 아래의 코드를 같이 살펴보면서 문제점도 같이 파악해보겠습니다. 전화번호를 저장하고 출력하는 프로그램입니다.

```
#include <stdio.h>
#include <string.h>

#define CAPACITY 100
#define BUFFER_SIZE 20

char * names[CAPACITY];
char * numbers[CAPACITY];
int n=0;

void add();
void find();
void status();
void delete();
void load();
void save();

int main(){
    char command[BUFFER_SIZE];

    while(1){
        printf("$ ");
        scanf("%s", command);

        if(strcmp(command, "add")==0)
            add();
        else if(strcmp(command, "find")==0)
            find();
        else if(strcmp(command, "status")==0)
            status();
        else if(strcmp(command, "delete")==0)
            delete();
        else if(strcmp(command, "load")==0)
            load();
        else if(strcmp(command, "save")==0)
            save();
        else if(strcmp(command, "exit")==0)
            break;
    }
}

void add(){
    char buffer1[BUFFER_SIZE], buffer2[BUFFER_SIZE];
    scanf("%s", buffer1);
    scanf("%s", buffer2);

    int i = n-1;

    while(i>=0 && strcmp(names[i], buffer1)>0){
        names[i+1] = names[i];
        numbers[i+1] = numbers[i];
        i--;
    }

    names[i+1] = strdup(buffer1);
    numbers[i+1] = strdup(buffer2);

    n++;

    printf("%s was added successfully. \n",buffer1);
}

void find(){
    char buffer[BUFFER_SIZE];
    scanf("%s", buffer);
    int i;
    for(i=0; i<n; i++){
        if(strcmp(buffer,names[i])==0){
            printf("%s\n", numbers[i]);
        }
    }
    printf("No person named '%s' exists.\n", buffer);
}

void status(){
    int i;
    for(i=0; i<n; i++)
        printf("%s %s\n", names[i], numbers[i]);
    printf("Total %d people.\n", n);
}

int search(char * name){
    int i;
    for(i=0; i<n; i++){
        if(strcmp(name, names[i])==0)
            return i;
    }
    return -1;
}

void delete(){
    char buffer[BUFFER_SIZE];
    scanf("%s", buffer);
    int index = search(buffer);
    if(index==-1)
        printf("No person named %s exists. \n", buffer);

    int i = index;

    for(; i<n-1; i++){
        names[i] = names[i+1];
        numbers[i] = numbers[i+1];
    }
    n--;
    printf("person named %s deleted successfully.\n", buffer);
}

void load(){
    char fileName[BUFFER_SIZE];
    char buffer1[BUFFER_SIZE];
    char buffer2[BUFFER_SIZE];

    scanf("%s", fileName);

    FILE * fp = fopen(fileName,"r");

    if(fp==NULL)
        printf("Open failed.\n");

    while(fscanf(fp,"%s",buffer1) != EOF){
        fscanf(fp, "%s", buffer2);
        names[n] = strdup(buffer1);
        numbers[n] = strdup(buffer2);
        n++;
    }

    fclose(fp);
}

void save(){
    int i;
    char fileName[BUFFER_SIZE];
    char tmp[BUFFER_SIZE];

    scanf("%s", tmp);
    scanf("%s", fileName);

    FILE * fp = fopen(fileName, "w");

    if(fp==NULL)
        printf("Open Failed.\n");
    for(i=0; i<n; i++)
        fprintf(fp, "%s %s\n", names[i], numbers[i]);

    fclose(fp);
}
```

위의 코드의 문제점은 한 단어씩 입력해야 한다는 것입니다.  
add kms 01099150000 이런 식으로 입력을 자연스럽게 받지 못합니다.  
add  
kms 01099150000 이렇게 두번에 걸쳐서 입력을 받아야 하지요.  
문자열 토크나이징이라는 것은 구분문자(delimiter)를 이용해서 긴 문자열을 작은 문자열로 자르는 일을 의미합니다.  
그리고 이렇게 잘라진 문자열을 토큰(token)이라고 합니다.  
C언어에서는 주로 strtok 함수를 이용합니다.  
  
![strtok](https://zerobugplz.github.io/images/studying/strtok.png)  
  
strtok의 첫 번째 인자로는 문자열의 시작 주소를, 두번째 인자로는 구분자의 시작 주소를 줍니다.  
주의할 점은 strtok는 원본 문자열을 변형시키므로 포인터로 가리키는 문자열은 인자로 받을 수 없습니다.  

```
str[] = "ajfiaoejfow" -> 가능
char * str = "ajifowjoeifwe" -> 불가능
```

처음만 저렇게 주고 두 번째부터는 첫 번째 인자로 NULL값을 줍니다(토큰으로 나눌 때 널값이 삽입되므로).  
아래는 사용예시입니다.  

```
#include <stdio.h>
#include <string.h>

int main(void){
    char str[] = "my # name # is # myeongsoo kim # ~!";
    char delim[] = "#";
    char *token;

    token = strtok(str, delim);
    while(token != NULL){
        printf("next token is: %s:%d\n", token, strlen(token));
        token = strtok(NULL, delim);
    }
    return 0;
}
```

이렇게 토크나이징을 이용해서 위의 코드를 개선해봤습니다.

```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

#define INIT_CAPACITY 3
#define BUFFER_SIZE 50

char ** names; // char * 타입의 배열의 이름이므로 이중포인터로 대체하였습니다
char ** numbers;

int capacity = INIT_CAPACITY;
int n=0;

char delim[] = " ";

void init_directory();
void process_command();

int main(){

    init_directory(); // 이 함수에서 배열 names와 numbers를 생성합니다
    process_command(); // 사용자의 명령을 받아 처리합니다

    return 0;
}

void reallocation(){
    int i;

    capacity *= 2;
    char **tmp1 = (char**)malloc(capacity * sizeof(capacity));
    char **tmp2 = (char**)malloc(capacity * sizeof(capacity));

    for(i=0; i<n; i++){
        tmp1[i] = names[i];
        tmp2[i] = numbers[i];
    }

    free(names);
    free(numbers);

    names = tmp1;
    numbers = tmp2;
}

void init_directory(){
    names = (char **)malloc(INIT_CAPACITY * sizeof(char*));
    numbers = (char**)malloc(INIT_CAPACITY * sizeof(char*));
}

int search(char * name){
    int i;
    for(i=0; i<n; i++){
        if(strcmp(name, names[i])==0)
            return i;
    }
    return -1;
}

int read_line(char str[], int limit){
    int ch, i=0;

    while((ch=getchar()) != '\n'){
        if(i < limit-1)
            str[i++] = ch;
    }
    str[i] = '\0';

    return i;
}

void add(char * name, char * number){
    if(n>=capacity)
        reallocation();
    int i=n-1;
    while(i>=0 && strcmp(names[i], name) > 0){
        names[i+1] = names[i];
        numbers[i+1] = numbers[i];
        i--;
    }

    names[i+1] = strdup(name);
    numbers[i+1] = strdup(number);
    n++;
}

void load(char *fileName){
    char buffer1[BUFFER_SIZE];
    char buffer2[BUFFER_SIZE];

    FILE * fp = fopen(fileName,"r");

    if(fp==NULL)
        printf("Open failed.\n");

    while(fscanf(fp,"%s",buffer1) != EOF){
        fscanf(fp, "%s", buffer2);
        add(buffer1, buffer2);
    }
    fclose(fp);
}

void status(){
    int i;
    for(i=0; i<n; i++)
        printf("%s %s\n", names[i], numbers[i]);
    printf("Total %d people.\n", n);
}

void delete(char * name){
    int i = search(name);

    if(i == -1)
        printf("No person named %s exists.\n", name);

    int j = i;
    for(; j<n-1; j++){
        names[j+1] = names[j];
        numbers[j+1] = numbers[j+1];
    }
    n--;
    printf("'%s' was deleted successfully.\n", name);
}

void save(char *fileName){
    int i;
    FILE * fp = fopen(fileName, "w");

    if(fp==NULL)
        printf("Open failed.\n");

    for(i=0; i<n; i++)
        fprintf(fp, "%s %s \n", names[i], numbers[i]);
    fclose(fp);
}

void find(char * name){
    int index = search(name);
    if(index == -1)
        printf("No name %s exists.\n", name);
    else
        printf("%s \n", numbers[index]);
}


void process_command(){
    char command_line[BUFFER_SIZE];
    char *command, *arg1, *arg2;

    while(1){
        printf("$ ");

        if(read_line(command_line, BUFFER_SIZE)<=0)
            continue;

        command = strtok(command_line, delim);
        if(command == NULL)
            continue;
        if(strcmp(command, "read")==0){
            arg1 = strtok(NULL, delim);
            if(arg1 == NULL){
                printf("File name required.\n");
                continue;
            }
            load(arg1);
        }
        else if(strcmp(command, "add") == 0){
            arg1 = strtok(NULL, delim);
            arg2 = strtok(NULL, delim);
            if(arg1 == NULL || arg2 == NULL){
                printf("Invalid arguments.\n");
                continue;
            }
            add(arg1, arg2);

            printf("%s was added successfully.\n", arg1);
        }

        else if(strcmp(command, "find") == 0){
            arg1 = strtok(NULL, delim);
            if(arg1 == NULL){
                printf("Invalid arguments.\n");
                continue;
            }
            find(arg1);
        }

        else if(strcmp(command, "status") == 0){
            status();
        }

        else if(strcmp(command, "delete") == 0){
            arg1 = strtok(NULL, delim);
            if(arg1 == NULL){
                printf("Invalid arguments.\n");
                continue;
            }
            delete(arg1);
        }

        else if(strcmp(command, "save") == 0){
            arg1 = strtok(NULL, delim);
            arg2 = strtok(NULL, delim);
            if(arg1 == NULL || strcmp(arg1, "as") != 0 || arg2 == NULL){
                printf("Invalid arguments.\n");
                continue;
            }
            save(arg2);

            printf("%s was saved successfully.\n", arg2);
        }

        else if(strcmp(command, "exit")==0)
            break;
    }
}
```

### 문자열 다른 형으로 변환

stdlib.h에는 문자열을 다른 형으로 변환시켜주는 함수들이 존재합니다.

|---
| 함수 | 설명
| :-: | :-:
| int atoi ( const char * str ); | str을 int로 변환한다.
| long int atol ( const char * str ); | str을 long으로 변환한다.
| double atof ( const char * str ); | str을 double으로 변환한다.

## 유니코드

### 유니코드 사용하기

다국어 지원은 참 매력적인 옵션입니다. 어느 프로그램을 만들던지 대부분은 최대한 많은 사람들이 사용해주었으면 좋겠고 혹은 영어권이 아닌 우리나라 같은 경우에는 기본적으로 제공되는 아스키코드만으로는 한국어를 표현할 수 없기 때문에 유니코드의 사용은 불가피합니다.  
하지만 C언어에서 유니코드를 처리하는 것은 매우 까다롭습니다. 비주얼스튜디오에서도 유니코드를 지원하고 있기는 하지만 말 그대로 비주얼스튜디오에 의존적이어야 가능합니다. 따라서 저는 C언어로 유니코드를 사용하는 것을 비추천합니다. 그럼 한국어는 사용할 수 없는 것일까요?  
아닙니다. 인터페이스는 파이썬과 같은 다른 언어로 꾸며주면 됩니다. 파이썬은 한국어를 매우 쉽게 지원하면서 C언어와 같이 사용하기가 쉽습니다. 프로그래밍의 성능이 중시되는 곳에는 C언어를 사용하고 나머지 영역인 인터페이스같은 곳들을 파이썬과 같은 유니코드 지원이 좋은 언어로 프로그래밍을 하는 것을 추천한다는 이야기입니다.