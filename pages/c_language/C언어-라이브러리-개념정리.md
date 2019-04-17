---
title: C언어 라이브러리 개념정리
keywords: C언어 라이브러리
last_updated: September 23, 2017
tags: [C언어]
summary: "C언어 라이브러리의 개념 소개와 만드는 방법입니다."
sidebar: c_language_sidebar
permalink: C언어-라이브러리-개념정리.html
folder: c_language
---

# 라이브러리

## 개념

라이브러리는 유용한 함수들의 모임입니다. 우리가 평소에 scanf와 printf를 사용할 수 있게 해주던 stdio도 마찬가지로 입력, 출력을 쉽게 해주는 함수들을 제공하는 라이브러리였습니다. 다양한 다른 프로그래머들이 만든 라이브러리를 통해 편하게 원하는 기능을 사용할 수 있는 경우가 많습니다. 혹은 자신이 직접 라이브러리를 만들어서 여러 프로그램에 적용시킬수도 있습니다.  
아래의 내용들은 [One Day One Line](http://killsia.tistory.com/entry/CC-library-만들기) 블로그의 저작권법을 준수하며 참고하였습니다.

### Library(라이브러리)

반복적으로 사용하는 기능들을 함수로 정의하여 필요할 때 마다 호출하여 사용하는 것이 좋습니다. 이러한 것들을 모아 놓은 것을 Library라고 합니다.  
library 는 보통 index(목차) + files(a.o + b.o + c.o + ....) 로 구성되어 있다고 볼 수 있습니다. unix/linux 에서 Library 파일은 일반적으로 lib 로 시작합니다.  
C언어 표준은 일반 프로그래머들이 공통적으로 사용할 만한 Library 들을 제공하며, 이런 standard library(표준 라이브러리)라고 합니다. 앞서 살펴본 stdio.h 등이 여기 속합니다.  
unix/linux에서 standard library 들은 보통 /lib, /usr/lib 에 존재하고 lib*.a(static library, 정적 라이브러리), lib*.so(shared library, 공유 라이브러리) 와 같은 file name을 가진다. a는 archive, so는 shared object를 뜻합니다.  
```
$ ar -tv libc.a // library 안에 있는 object file(*.o) 의 목록을 확인할 수 있다. 참고로, libc.a는 compile 시 자동으로 link되는 standard library 파일 중 하나이다.
$ ar -tv libc.a | grep -e scanf -e printf // scanf, printf와 관련된 object file들만 볼 수도 있다.
```
### header file

C/C++ 에서 library를 사용하기 위해서는 header file 과 library 파일이 필요합니다. header file은 #include 라는 preprocess keyword 에 따라 source file에 포함되며 컴파일시 필요합니다. gcc의 -I 옵션으로 추가할 수 있다. library는 compiler에 의해 link되며, -L, -l 옵션을 이용하여 추가할 수 있습니다.  

compiler는 헤더파일을 참조하고, library 파일을 link하여 프로그램을 compile한다.  

### static library ( 정적 라이브러리 )

static library 는 object file(*.o) 들의 단순한 모음입니다. 보통 lib*.a 와 같은 형태의 file name을 가집니다. standard library 의 *.a 파일들은 보통 /usr/lib 에 위치합니다. static library 의 code는 링크단계에서 실행파일에 포함되므로 한번 만든 실행파일에 해당되는 라이브러리 파일을 아무리 수정해도 실행파일에는 영향을 미치지 않습니다.

### shared library ( 공유 라이브러리 )

shared library는 static library와 달리 프로그램 실행시 loading 됩니다. static library와 달리 compile 시 실행파일에 포함되는 것이 아니기 때문에 프로그램의 크기는 작아지지만, 실행 시 shared library를 loading 하는데 시간이 필요하여 static library를 이용했을 때 보다 약간 느릴 수 있습니다. 하지만 라이브러리에서 수정된 내용을 실행파일이 즉시 로딩하여 반영하므로 요새는 공유 라이브러리를, 즉 동적 라이브러리를 사용하는 것이 대세입니다.

shared library 를 사용하는 프로세스들은 이미 memory 에 load 된 하나의 shared library를 공유해서 사용하므로 memory 를 절약할 수 있습니다(웹이나 앱등 고수준의 프로그래밍을 하시는 분들은 CDN 캐싱을 생각하시면 될 것 같습니다).

## C언어 라이브러리 만들기

### static library 만들기

먼저 object file 을 만듭니다.
```
$ gcc -c file1.c
$ gcc -c file2.c
$ gcc -c file3.c
```

ar(ARchive) command 를 이용해서 *.a 를 만듭니다.
```
$ ar -r libtest.a file1.o
$ ar -r libtest.a file2.o
$ ar -r libtest.a file3.o
```
archive 파일의 내용을 확인합니다.
```
$ ar -tv libtest.a
```
Library 를 참조하여 프로그램을 compile합니다.
```
$ gcc -o myprogram myprogram.c -L. -ltest
```

### ar command options

- -d : archive 로 부터 file을 삭제
- -q : 이미 존재하고 있더라도 archive의 끝에 file을 append
- -r : 파일이 archive 내에 존재하지 않으면 추가하고, 존재하면 현재 버전으로 replace
- -t : stdout 으로 archive의 목차를 보여 준다.
- -x : archive 로 부터 파일들을 현재의 directory 로 복사
- -v : 출력을 확인하고 싶을 경우 사용

### shared library 만들기

먼저 object file 을 만듭니다. -b -ePIC 옵션은 위치(address)에 독립적인 code를 생성합니다.
```
$ gcc -b -ePIC -c file1.c
$ gcc -b -ePIC -c file2.c
$ gcc -b -ePIC -c file3.c
```

shared library file 생성
```
$ gcc -b -o libtest.so file1.o file2.o file3.o
```
static library와 동일한 방법으로 library 를 참조하여 프로그램을 compile 후 실행하면 됩니다.

### ldd command

binary 파일이 요구하는 shared library 목록을 알아 볼 때 사용됩니다.

```
$ ldd myprogram
```

### LD_LIBRARY_PATH를 이용한 shared library 참조

LD_LIBRARY_PATH 라는 환경 변수(Environment Variable)를 이용하여 shared library의 경로를 추가할 수 있습니다.
```
$ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/myhome/mylib
```