---
title: "[백준 알고리즘 강의 문제 시리즈 - 5] 1406번 : 에디터"
date: 2023-01-10 09:43:00 +0900
categories: [백준, 백준 알고리즘 강의 문제 시리즈]
tags: [devrunner, BOJ, C++, 백준, 알고리즘 기초 1, 자료구조, 스택, BOJ 1406]
---

## **링크**

---

<https://www.acmicpc.net/problem/1406>

## **문제 접근 방법**

---

에디터의 커서를 명령어를 통해 조작해 최종 출력값을 도출해야 하는 문제이다.

아래와 같은 구조로 설계해 프로그램을 짰다.

![editor](https://user-images.githubusercontent.com/87963766/211434565-d5af04c9-d8d5-41eb-815d-3996f2f283de.png)

<center>에디터 출력 상태</center>

![stack](https://user-images.githubusercontent.com/87963766/211434996-8198bef0-356c-411c-a000-4d5c982466cf.png)

<center>스택 상태</center>

해당 구조를 사용해 문제에서 주어지는 명령어들을 쉽게 구현할 수 있다.

문제를 처음 봤을 때 직관적으로 연결 리스트를 이용해서 풀 수 있지 않을까? 라는 생각이 먼저 드는 문제다. 하지만 이와 같이 스택을 이용하면 더 쉽게 풀 수 있다.

## **코드**

---

```cpp
#include <bits/stdc++.h>
using namespace std;

int n;
// 각각 커서의 왼쪽과 오른쪽에 있는 글자들을 저장할 스택
stack<char> left_stk, right_stk;

void input() {
  string str;

  cin >> str;

  for (char c : str) {
    left_stk.push(c);
  }
}

void L() {
  if (!left_stk.empty()) {
    right_stk.push(left_stk.top());
    left_stk.pop();
  }

  return;
}

void D() {
  if (!right_stk.empty()) {
    left_stk.push(right_stk.top());
    right_stk.pop();
  }

  return;
}

void B() {
  if (!left_stk.empty()) {
    left_stk.pop();
  }
}

void P(char c) { left_stk.push(c); }

void output() {
  while (!left_stk.empty()) {
    L();
  }

  while (!right_stk.empty()) {
    cout << right_stk.top();
    right_stk.pop();
  }
}

int main() {
  ios_base::sync_with_stdio(false);
  cin.tie(NULL);
  cout.tie(NULL);
  // c++의 표준 stream의 동기화를 끊는 역할을 하여 입출력의 속도를 높인다.

  input();

  cin >> n;

  for (int i = 0; i < n; ++i) {
    char command;
    char c;

    cin >> command;

    switch (command) {
    case 'L':
      L();
      break;

    case 'D':
      D();
      break;

    case 'B':
      B();
      break;

    case 'P':
      cin >> c;
      P(c);
      break;
    }
  }

  output();

  return 0;
}
```

## **인증**

---

![image](https://user-images.githubusercontent.com/87963766/211433829-94853f36-6840-4712-be5d-5621e10daf33.png)
