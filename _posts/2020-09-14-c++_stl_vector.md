---
title: C++ STL - Vector
author: Jade Bright
date: 2020-09-14 20:16:00 +0900
categories: [C++]
tags: [C++STL]
---

## Header
```c++
#inlcude <vector>
```
## 생성

vector<data_type> v

vector<data_type> v(size, val)

## 함수

amout 수 만큼 val 값으로 초기화: assgin(amout, val)

맨 뒤에 원소 삽입: push_back(val)

해당 iter에 원소 삽입: insert(iter, amount, val), insert(iter, val)

맨 앞 값 반환: front()

맨 앞 iter 반환: begin()

맨 뒤 값 반환: back()

맨 뒤 다음 iter 반환: end()

맨 앞 reverse_iter 반환(reverse_iter는 맨 뒤부터 역순 으로 탐색): v.rbegin()

맨 뒤 다음 reverse_iter 반환: v.rend()

맨 뒤 원소 제거: push_pop()

해당 iter 원소 제거: erase(iter)

크기 반환: size()

메모리 할당 크기 반환: capacity()

비었는지 여부 확인: empty()

비우기: clear()

amount 수로 크기 조절 크기가 증가한다면 초기값은 val: resize(amount, val)

## 예제
```c++
#include<iostream>
#include<vector>

using namespace std;

int main()
{

	vector<int> v;
	v.assign(10, 10);
	//vector<int> v(10, 10);
	v.push_back(1);
	v.push_back(2);
	v.push_back(3);
	v.insert(--v.end(), 4); // end()는 마지막 원소의 다음 메모리 주소이기 때문에 --필요
	v.insert(--v.end(), 2, 5);
	cout << v[10] << " " << v.at(10) << endl;
	cout << v.front() << " " << v.back() << endl;
	cout << *v.begin() << " " << *(--v.end()) << endl;
	cout << *v.rbegin() << " " << *(--v.rend()) << endl;
	v.pop_back();
	cout << v.back() << endl;
	v.erase(--v.end());
	cout << v.back() << endl;
	cout << v.size() << " " << v.capacity() << endl;
	v.resize(20, 5);
	cout << v.size() << " " << v.capacity() << endl;
	v.clear();
	cout << v.size() << " " << v.empty() << endl;

	return 0;
}
```