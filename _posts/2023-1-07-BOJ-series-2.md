---
title: "[백준 알고리즘 강의 문제 시리즈 - 2] 9093번 : 단어 뒤집기"
date: 2023-01-08 00:34:00 +0900
categories: [백준, 백준 알고리즘 강의 문제 시리즈]
tags: [devrunner, BOJ, C++, 백준, 알고리즘 기초 1, 자료구조, 스택, BOJ 9093]
---

## 링크

---

<https://www.acmicpc.net/problem/9093>

## 문제 접근 방법

---

문제에서 문장의 각 단어들의 순서를 바꾸는 것을 요구하고 있다.

각 단어의 문자들을 선입후출(FILO)의 자료구조인 스택에 저장한 후, 단어의 끝 문자까지 모두 넣었을 경우 다시 하나씩 빼내어 단어의 첫 글자의 위치부터 다시 저장한다.

이 과정을 문장의 모든 단어들에 대해 반복한다.

이 때, 문장을 모두 읽었을 때, 스택에 저장된 문자들을 잊어서는 안된다.

이번 문제에서도 스택 자료구조를 따로 구현했다.
다만 앞서 풀었던 문제와의 차이점은 템플릿을 썼다는 점이다.
클래스나 구조체의 활용성을 높이고 싶다면 템플릿을 쓰는 것이 많이 도움이 된다.
다만 여기서는 굳이 그럴 필요는 없었던 듯하다.

## 코드

```cpp
#include <iostream>
#include <string>
using namespace std;

template <typename T> class Stack {
  struct node {
    T num;
    node *next;
  };
  using link = node *;

  link top;

public:
  Stack() : top(NULL) {}
  void Push(T x);
  T Pop();
  ~Stack();
};

int main() {
  ios_base::sync_with_stdio(false);
  cin.tie(NULL);
  cout.tie(NULL);
  // c++의 표준 stream의 동기화를 끊는 역할을 하여 입출력의 속도를 높인다.

  int n;
  cin >> n;

  // 테스트 케이스를 입력 받은 후 다음 버퍼를 비워줘야 실행이 제대로 된다.
  cin.ignore();
  /*
  예전에 풀었을 때는 아래와 같이 임시 방편으로 string 변수를 따로 만들어
  버렸는데, 이번 포스팅을 하면서 찾아보니 위 코드를 써서 버퍼를 비우는 방법이
  있었다.
  */
  // string trash;
  // getline(cin,trash);

  for (int i = 0; i < n; i++) {
    Stack<char> stack;

    string str;
    getline(cin, str);

    // str 내의 각 단어의 첫 시작 문자의 index이다.
    int start = 0;

    // str을 처음부터 끝까지 훑으며 각 단어를 뒤집어 저장하는 과정이다.
    for (int j = 0; j < str.length(); j++) {
      /*
      현재 index에 저장된 문자가 공백일 시,
      현재 스택에 저장된 문자들을 하나씩 꺼내 start부터 차례대로 저장
      이 과정에서 단어가 뒤집혀 저장된다.
      */
      if (str[j] == ' ') {
        for (int k = start; k < j; k++) {
          str[k] = stack.Pop();
        }
        // start 값 갱신
        start = j + 1;
      }

      // 그 외의 경우 문자를 스택에 넣기
      else {
        stack.Push(str[j]);
      }
    }

    // 문장을 끝까지 훑었을 시 스택에 저장된 문자들 모두 꺼내기
    for (int j = start; j < str.length(); j++) {
      str[j] = stack.Pop();
    }

    cout << str << '\n';
  }

  return 0;
}

template <typename T> void Stack<T>::Push(T x) {
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
}

template <typename T> T Stack<T>::Pop() {
  int tmp = top->num;
  top = top->next;

  return tmp;
}

template <typename T> Stack<T>::~Stack() {
  while (top) {
    link tmp = top;
    top = top->next;
    delete tmp;
  }
}
```

## 인증

---

![cert](https://user-images.githubusercontent.com/87963766/211158450-778ff8f2-558b-4cda-af3f-51a7b686b94c.png)
