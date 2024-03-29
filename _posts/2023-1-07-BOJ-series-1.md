---
title: "[백준 알고리즘 강의 문제 시리즈 - 1] 10828번 : 스택"
date: 2023-01-07 00:15:00 +0900
categories: [백준, 백준 알고리즘 강의 문제 시리즈]
tags: [devrunner, BOJ, C++, 백준, 알고리즘 기초 1, 자료구조, 스택, BOJ 10828]
---

## **링크**

---

<https://www.acmicpc.net/problem/10828>

## **문제 접근 방법**

---

자료구조를 배웠다면 쉽게 풀 수 있는 문제다.
stack을 이용해 풀 수 있는 문제인데, C++ STL에 구현된 stack을 이용해 풀어도 되지만, 난 그냥 클래스를 따로 구현하여 문제를 풀었다.

## **코드**

---

```cpp
#include <iostream>
#include <string>
using namespace std;

// 문제에 주어진 조건대로 스택 클래스 구현
class Stack {
  struct node {
    int num;
    node *next;
  };
  using link = node *;

  link top;
  int size;

public:
  Stack() : top(NULL), size(0) {}
  void Push(int x);
  void Pop();
  void Size();
  void Empty();
  void Top();
  ~Stack();
};

int main() {
  ios_base::sync_with_stdio(false);
  cin.tie(NULL);
  cout.tie(NULL);
  // c++의 표준 stream의 동기화를 끊는 역할을 하여 입출력의 속도를 높인다.

  int n;
  cin >> n;

  Stack stack;

  for (int i = 0; i < n; i++) {
    string tmpstr;
    cin >> tmpstr;

    if (tmpstr == "push") {
      int tmpn;
      cin >> tmpn;

      stack.Push(tmpn);
    } else if (tmpstr == "pop") {
      stack.Pop();
    } else if (tmpstr == "size") {
      stack.Size();
    } else if (tmpstr == "empty") {
      stack.Empty();
    } else if (tmpstr == "top") {
      stack.Top();
    }
  }

  return 0;
}

void Stack::Push(int x) {
  if (top == NULL) {
    top = new node;
    top->num = x;
    top->next = NULL;
  } else {
    link tmp = new node;
    tmp->num = x;
    tmp->next = top;
    top = tmp;
  }

  size++;
}

void Stack::Pop() {
  if (size == 0) {
    cout << -1 << '\n';
  } else {
    int tmp = top->num;
    link tmpnod = top;
    top = top->next;
    delete tmpnod;
    size--;

    cout << tmp << '\n';
  }
}

void Stack::Size() { cout << size << '\n'; }

void Stack::Empty() {
  if (size == 0) {
    cout << 1 << '\n';
  } else {
    cout << 0 << '\n';
  }
}

void Stack::Top() {
  if (size == 0) {
    cout << -1 << '\n';
  } else {
    cout << top->num << '\n';
  }
}

Stack::~Stack() {
  while (top) {
    link tmp = top;
    top = top->next;
    delete tmp;
  }
}
```

## **인증**

---

![cert](https://user-images.githubusercontent.com/87963766/211056721-ba6906a0-06e0-42c5-beb3-2b26707f47ee.png)
