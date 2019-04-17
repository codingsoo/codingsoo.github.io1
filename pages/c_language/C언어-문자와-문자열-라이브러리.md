---
title: C언어 문자, 문자열 처리 라이브러리
keywords: C언어 문자 처리 라이브러리, C언어 문자열 처리 라이브러리
last_updated: September 23, 2017
tags: [C언어]
summary: "C언어 문자, 문자열 처리 라이브러리에 대한 이야기"
sidebar: c_language_sidebar
permalink: C언어-문자와-문자열-라이브러리.html
folder: c_language
---

## 문자 처리 라이브러리

### ctype.h

C 언어의 표준 라이브러리로, 문자들을 조건에 맞는지 검사하고 변환하는 함수들을 포함하고 있습니다. 크게 문자 검사와 문자 변환 함수들로 나뉘어 있습니다.  

**문자 검사**  

```
int isalnum ( int c );	// c가 알파벳 또는 숫자이면 0이 아닌 값을 반환한다.

int isalpha ( int c );	// c가 알파벳이면 0이 아닌 값을 반환한다.

int iscntrl ( int c );	// c가 제어 문자이면 0이 아닌 값을 반환한다.

int isdigit ( int c );	// c가 숫자이면 0이 아닌 값을 반환한다.

int isgraph ( int c );	// c가 그래픽 문자이면 0이 아닌 값을 반환한다.

int islower ( int c );	// c가 소문자이면 0이 아닌 값을 반환한다.

int isprint ( int c );	// c가 출력할 수 있는 문자이면 0이 아닌 값을 반환한다.

int ispunct ( int c );	// c가 구두점 문자이면 0이 아닌 값을 반환한다.

int isspace ( int c );	// c가 공백 문자이면 0이 아닌 값을 반환한다.

int isupper ( int c );	// c가 대문자이면 0이 아닌 값을 반환한다.

int isxdigit ( int c );	// c가 16진 숫자이면 0이 아닌 값을 반환한다.
```

**문자 변환**  

```
int tolower ( int c );	    // c를 소문자로 변환한다.

int toupper ( int c );	    // c를 대문자로 변환한다.

int toascii ( int c );    // c를 아스키 코드로 변환한다.
```

## 문자열 처리 라이브러리

### string.h

string.h는 C 언어의 표준 라이브러리로, 메모리 블록이나 문자열을 다룰 수 있는 함수들을 포함하고 있습니다.
|---
| 함수 | 설명
| :-: | :-:
| char * strcpy ( char * destination, const char * source );| source를 destination에 복사한다.
| char * strncpy ( char * destination, const char * source, size_t num ) | source에서 destination으로 처음 num개의 문자들을 복사한다.
| char * strcat ( char * destination, const char * source ); | source를 destination뒤에 붙인다.
| char * strncat ( char * destination, char * source, size_t num ); | source에서 destination뒤에 처음 num개의 문자들을 붙인다.
| int strcmp ( const char * str1, const char * str2 ); | str1과 str2를 비교한다.
| int strncmp ( const char * str1, const char * str2, size_t num ); | str1의 처음 num개의 문자를 str2의 처음 num개의 문자와 비교한다.
| char * strchr ( const char * str, int character ); | str에서 처음으로 character와 일치하는 문자의 주소를 반환한다.
| size_t strcspn ( const char * str1, const char * str2 ); | str2에 들어있는 문자들 중 str1에 들어있는 문자와 일치하는 것이 있다면 첫 번째로 일치하는 문자까지 읽어들인 수를 반환한다.
| char * strchr ( const char * str, int character ); | str에서 마지막으로 character와 일치하는 문자의 주소를 반환한다.
| char * strstr ( const char * str1, const char * str2 ); | str1에서 str2를 검색하여 가장 먼저 나타나는 곳의 위치를 반환한다.
char * strtok ( char * str, const char * delimiters ); | str1을 delimiters의 문자들로 분리한다.
| size_t strlen ( const char * str ); | str의 길이를 반환한다.

### stdlib.h

stdlib.h에는 문자열을 다른 형으로 변환시켜주는 함수들이 존재합니다.

|---
| 함수 | 설명
| :-: | :-:
| int atoi ( const char * str ); | str을 int로 변환한다.
| long int atol ( const char * str ); | str을 long으로 변환한다.
| double atof ( const char * str ); | str을 double으로 변환한다.