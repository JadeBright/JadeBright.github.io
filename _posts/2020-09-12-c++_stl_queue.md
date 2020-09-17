---
title: C++ STL - Queue
author: Jade Bright
date: 2020-09-12 21:11:00 +0900
categories: [C++]
tags: [C++STL]
---

## Header
```c++
#inlcude <queue>
```
## 생성

일반 큐: queue<data_type> q, queue<data_type, container_type> q

우선순위 큐:  priority_queue<data_type> q, priority_queue<data_type, container_type, compare> q

## 함수

삽입: push(val)

삭제: pop()

처음 원소 조회(일반 큐): front() - data_type을 반환

마지막 원소 조회(일반 큐): back() - data_type을 반환

처음 원소 조회(우선순위 큐):  top() - data_type을 반환

큐가 비어있는 여부를 조사: empty() - bool을 반환

원소의 개수 조사: size() - size_type을 반환

## 예제
```c++
//Header
#include<iostream>
#include<queue>
#include<vector>
#include<tuple>

using namespace std;

struct compare
{
	bool operator()(pair<int, int>& a, pair<int, int>& b)
	{
		return (a.first + a.second) < (b.first + b.second);
	}
};

int main()
{
	//생성

	queue<int> q;
	//queue<int> q;
	priority_queue<int, vector<int>, greater<int> > pq;//오름차순 내림차순은 less
	//priority_queue<int> pq; 내림차순이 기본

	//함수
	q.empty();
	q.push(1);
	cout << q.size() << endl;
	cout << q.empty() << endl; //0: false, 1: true
	q.push(2);
	cout << q.size() << endl;
	cout << pq.empty() << endl;
	pq.push(1);
	cout << pq.size() << endl;
	cout << pq.empty() << endl;
	pq.push(2);
	cout << pq.size() << endl;
	cout << q.back() << endl;
	cout << q.front() << endl;
	cout << pq.top() << endl;
	q.pop();
	cout << q.size() << endl;
	pq.pop();
	cout << pq.size() << endl;

	//pair 사용
	queue<pair<int, int>> q2;
	q2.push(make_pair(1, 2));
	q2.push(pair<int, int>(3, 4));
	q2.push({ 5, 6 });
	cout << q2.front().first << " " << q2.front().second << endl;

	//tuple 사용
	queue<tuple<int, int, int> > q3;
	q3.push(make_tuple(1, 2, 3));
	cout << get<0>(q3.front()) << " " << get<1>(q3.front()) << " " << get<2>(q3.front()) << endl;
	int a, b, c;
	tie(a, b, c) = q3.front();
	cout << a << " " << b << " " << c << endl;
	//tie(a, b, ignore) = q3.front(); 마지막 원소는 생략

	//compare 사용
	priority_queue<pair<int, int>, vector<pair<int, int> >, compare > pq2;
	pq2.push({ 1, 7 });
	pq2.push({ 2, 4 });
	cout << pq2.top().first << " " << pq2.top().second << endl;
	pq2.pop();
	cout << pq2.top().first << " " << pq2.top().second << endl;

	return 0;
}
```