---
title: "[백준 알고리즘 강의 문제 시리즈 - 4] 1874번 : 스택 수열"
date: 2023-01-09 09:42:00 +0900
categories: [백준, 백준 알고리즘 강의 문제 시리즈]
tags: [devrunner, BOJ, C++, 백준, 알고리즘 기초 1, 자료구조, 스택, BOJ 1874]
---

## **링크**

---

<https://www.acmicpc.net/problem/1874>

## **문제 접근 방법**

---

1부터 n까지의 수에 대해 스택 작업을 수행하여 입력된 수열들을 어떻게 만들 수 있는 지, 또는 만들 수 없는 경우 NO를 출력하는 문제이다.
풀이 과정은 다음과 같다.

1. 입력된 수열을 하나씩 스캔하면서 해당 수까지 스택에 Push 작업을 진행한다. Push 작업을 수행하면서 스택에 Push하는 수(코드에서는 변수 k)의 크기를 1씩 증가시켜야 한다.

2. 스택의 Top에 있는 변수값이 현재 수열의 수와 동일할 시 Pop 작업을 수행한다.

3. 출력값은 2,3번 작업 실행 시 command 큐에 동시에 저장된다.

4. 동일하지 않을 경우 입력된 수열을 만들 수 없다.

5. 2~3까지의 과정을 수행하는 함수가 check이다. check 함수는 수열을 만들 수 있을 시 1을 반환하며, 그렇지 않을 경우 0을 반환한다.

6. main 함수에서 수열을 입력 받고 check 함수를 실행하여 결과를 출력한다.

이번에는 C++의 STL에 있는 라이브러리를 적극 활용했다. 앞으로도 이런 식으로 코드를 다시 짜볼 생각이다.

## **코드**

---

```cpp
#include <bits/stdc++.h>
using namespace std;

int n;
// 수열을 입력받을 벡터
vector<int> seq;
// 입력받은 수열을 만들 스택
stack<int> stk;
// 스택 연산을 저장할 큐
queue<char> command;

int check() {
  // 스택 작업에 이용될 변수
  int k = 0;

  for (int i = 0; i < n; ++i) {
    // k가 수열의 i번째 수보다 같아질 때 까지 값을 늘려가며 스택에 push.
    // 동시에 스택 작업 기록
    while (k < seq[i]) {
      ++k;
      stk.push(k);
      command.push('+');
    }

    // 위 작업이 끝난 후 수열의 i번째 수와 스택의 가장 위에 있는 수가 같을 시
    // pop 역시 동시에 스택 작업 기록
    if (seq[i] == stk.top()) {
      stk.pop();
      command.push('-');
    }
    // 같지 않다면 수열을 만드는 것이 불가능 함.
    else {
      return 0;
    }
  }

  return 1;
}

int main() {
  ios_base::sync_with_stdio(false);
  cin.tie(NULL);
  cout.tie(NULL);
  // c++의 표준 stream의 동기화를 끊는 역할을 하여 입출력의 속도를 높인다.

  cin >> n;

  for (int i = 0; i < n; i++) {
    int tmp;
    cin >> tmp;
    seq.push_back(tmp);
  }

  // check의 반환값으로 입력받은 수열을 만드는 것이 가능한 지의 여부 판단 가능
  if (check()) {
    while (!command.empty()) {
      cout << command.front() << '\n';
      command.pop();
    }
  } else {
    cout << "NO" << '\n';
  }

  return 0;
}
```

## **인증**

---

![image](https://user-images.githubusercontent.com/87963766/211426790-214e401a-4103-4244-8f22-7f469d5d7246.png)
