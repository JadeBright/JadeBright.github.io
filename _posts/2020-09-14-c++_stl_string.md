---
title: C++ STL - String
author: Jade Bright
date: 2020-09-15 21:16:00 +0900
categories: [C++]
tags: [C++STL]
---

## Header
```c++
#inlcude <string>
```
## 생성

string s;

## 함수

맨 앞 문자 반환: front()

맨 뒤 문자 반환: back()

맨 앞 iter 반환: begin()

맨 뒤 다음 iter 반환: end()

pos부터 str 삽입: insert(pos, str)

pos부터 size만큼 삭제: erase(pos, size)

맨 뒤 삽입: push_back(character)

맨 뒤 삭제: pop_back(character)

크기 반환: size()

길이 반환: length()

메모리 크기 반환: capacity()

size의 크기로 변환: resize(size, character) - 크기가 커질 때 나머지 공간을 character로 채움

pos부터 str과 일치하는 문자열 찾아 위치 반환: find(str, pos)

pos부터 size 크기만큼 반환: substr(pos, size)

str과 바꾸기: swap(&str)

비우기: clear()

비어있는지 여부 확인: empty()

## 예제
```c++
#include <string>
#include <iostream>
using namespace std;

int main()
{
    string s = "examples";
    cout << s.front() << " " << s.back() << endl;
    cout << *s.begin() << " " << *(--s.end()) << endl;
    s.insert(1, "1234");
    cout << s << endl;
    s.erase(1, 4);
    cout << s << endl;
    s.push_back('1');
    cout << s << endl;
    s.pop_back();
    cout << s << endl;
    cout << s.size() << " " << s.length() << " " << s.capacity() << endl;
    s.resize(6);
    cout << s << endl;
    s.resize(8, '1');
    cout << s << endl;
    cout << s.substr(s.find("ex", 0), 2) << endl;
    string tmp = "other";
    s.swap(tmp);
    cout << s << endl;
    s.clear();
    cout << s.empty() << endl;
    return 0;
}

```