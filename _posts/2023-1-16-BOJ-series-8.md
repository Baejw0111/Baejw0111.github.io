---
title: "[백준 알고리즘 강의 문제 시리즈 - 8] 10866번 : 덱"
date: 2023-01-16 09:14:00 +0900
categories: [백준, 백준 알고리즘 강의 문제 시리즈]
tags: [devrunner, BOJ, C++, 백준, 알고리즘 기초 1, 자료구조, 덱, BOJ 10866]
---

## **링크**

---

<https://www.acmicpc.net/problem/10866>

## **문제 접근 방법**

---

자료구조의 한 종류인 "덱(Deque)"을 구현하는 문제이다. 해당 자료구조 역시 C++ STL에 구현되어 있으며, 해당 문제는 앞서 풀었던 [스택](https://baejw0111.github.io/posts/BOJ-series-1-10828/), [큐](https://baejw0111.github.io/posts/BOJ-series-6-10845/) 문제와 같이 구현에 의미가 있는 문제이기에 STL을 사용하지 않고 직접 구현하여 풀었다.

참고로 Deque은 Double-Ended Queue의 줄임말로, 이름에서 알 수 있는 것처럼 구조는 다음과 같은 구조이다.

![image](https://user-images.githubusercontent.com/87963766/212588419-7529c058-1780-431e-a32c-e67e11710267.png)

###### <center>큐의 양쪽에서 엘리먼트의 삽입과 삭제를 수행할 수 있다.<center>

## **코드**

---

<details>
<summary>펼치기</summary>
<div markdown="1">

```cpp
#include <bits/stdc++.h>
using namespace std;

class Deque {
  struct node {
    int num;
    node *prev, *next;
  };
  using link = node *;

  link head, tail;
  int size;

public:
  Deque();
  void Push_Front(int x);
  void Push_Back(int x);
  void Pop_Front();
  void Pop_Back();
  void Size();
  void Empty();
  void Front();
  void Back();
  ~Deque();
};

int main() {
  int n;
  cin >> n;

  Deque que;

  for (int i = 0; i < n; i++) {
    string tmpstr;
    cin >> tmpstr;

    if (tmpstr == "push_front") {
      int tmpn;
      cin >> tmpn;

      que.Push_Front(tmpn);
    } else if (tmpstr == "push_back") {
      int tmpn;
      cin >> tmpn;

      que.Push_Back(tmpn);
    } else if (tmpstr == "pop_front") {
      que.Pop_Front();
    } else if (tmpstr == "pop_back") {
      que.Pop_Back();
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

Deque::Deque() : head(new node), tail(new node), size(0) {
  head->prev = NULL;
  head->next = tail;

  tail->prev = head;
  tail->next = NULL;
}

void Deque::Push_Front(int x) {
  link tmp = new node;

  tmp->num = x;

  tmp->prev = head;
  tmp->next = head->next;

  head->next = tmp;
  tmp->next->prev = tmp;

  size++;
}

void Deque::Push_Back(int x) {
  link tmp = new node;

  tmp->num = x;

  tmp->prev = tail->prev;
  tmp->next = tail;

  tail->prev = tmp;
  tmp->prev->next = tmp;

  size++;
}

void Deque::Pop_Front() {
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

void Deque::Pop_Back() {
  if (size == 0) {
    cout << -1 << '\n';
  } else {
    link tmpnod = tail->prev;
    int tmp = tmpnod->num;

    tail->prev = tmpnod->prev;
    tail->prev->next = tail;

    delete tmpnod;
    size--;

    cout << tmp << '\n';
  }
}

void Deque::Size() { cout << size << '\n'; }

void Deque::Empty() {
  if (size == 0) {
    cout << 1 << '\n';
  } else {
    cout << 0 << '\n';
  }
}

void Deque::Front() {
  if (size == 0) {
    cout << -1 << '\n';
  } else {
    cout << head->next->num << '\n';
  }
}

void Deque::Back() {
  if (size == 0) {
    cout << -1 << '\n';
  } else {
    cout << tail->prev->num << '\n';
  }
}

Deque::~Deque() {
  tail = NULL;

  while (head) {
    link tmp = head;
    head = head->next;
    delete tmp;
  }
}
```

</div>
</details>

## **인증**

---

![image](https://user-images.githubusercontent.com/87963766/212574995-03a2e3e8-3f00-4c67-a3bf-0ad542ffc1c1.png)
