---
title: "[백준 알고리즘 강의 문제 시리즈 - 6] 10845번 : 큐"
date: 2023-01-11 13:27:00 +0900
categories: [백준, 백준 알고리즘 강의 문제 시리즈]
tags: [devrunner, BOJ, C++, 백준, 알고리즘 기초 1, 자료구조, 큐, BOJ 10845]
---

## **링크**

---

<https://www.acmicpc.net/problem/10845>

## **문제 접근 방법**

---

문제에서 요구하는 것처럼 큐를 구현하는 문제다.

C++의 STL에 있는 큐를 사용해도 되지만 구현의 의미가 큰 문제이기 때문에 따로 클래스를 만들어 구현했다.

## **코드**

---

```cpp
#include <bits/stdc++.h>
using namespace std;

class Queue {
  struct node {
    int num;
    node *prev, *next;
  };
  using link = node *;

  link head, tail;
  int size;

public:
  Queue();
  void Push(int x);
  void Pop();
  void Size();
  void Empty();
  void Front();
  void Back();
  ~Queue();
};

int main() {
  ios_base::sync_with_stdio(false);
  cin.tie(NULL);
  cout.tie(NULL);
  // c++의 표준 stream의 동기화를 끊는 역할을 하여 입출력의 속도를 높인다.

  int n;
  cin >> n;

  Queue que;

  for (int i = 0; i < n; i++) {
    string tmpstr;
    cin >> tmpstr;

    if (tmpstr == "push") {
      int tmpn;
      cin >> tmpn;

      que.Push(tmpn);
    } else if (tmpstr == "pop") {
      que.Pop();
    } else if (tmpstr == "size") {
      que.Size();
    } else if (tmpstr == "empty") {
      que.Empty();
    } else if (tmpstr == "front") {
      que.Front();
    } else if (tmpstr == "back") {
      que.Back();
    }
  }

  return 0;
}

Queue::Queue() : head(new node), tail(new node), size(0) {
  head->prev = NULL;
  head->next = tail;

  tail->prev = head;
  tail->next = NULL;
}

void Queue::Push(int x) {
  link tmp = new node;

  tmp->num = x;

  tmp->prev = tail->prev;
  tmp->next = tail;

  tail->prev = tmp;
  tmp->prev->next = tmp;

  size++;
}

void Queue::Pop() {
  if (size == 0) {
    cout << -1 << '\n';
  } else {
    link tmpnod = head->next;
    int tmp = tmpnod->num;

    head->next = tmpnod->next;
    head->next->prev = head;

    delete tmpnod;
    size--;

    cout << tmp << '\n';
  }
}

void Queue::Size() { cout << size << '\n'; }

void Queue::Empty() {
  if (size == 0) {
    cout << 1 << '\n';
  } else {
    cout << 0 << '\n';
  }
}

void Queue::Front() {
  if (size == 0) {
    cout << -1 << '\n';
  } else {
    cout << head->next->num << '\n';
  }
}

void Queue::Back() {
  if (size == 0) {
    cout << -1 << '\n';
  } else {
    cout << tail->prev->num << '\n';
  }
}

Queue::~Queue() {
  tail = NULL;

  while (head) {
    link tmp = head;
    head = head->next;
    delete tmp;
  }
}
```

## **인증**

![image](https://user-images.githubusercontent.com/87963766/211717171-31236044-4e9c-40c8-b6f0-caebe1801e86.png)
