---
title: "[백준 알고리즘 강의 문제 시리즈 - 9] 17413번 : 단어 뒤집기 2"
date: 2023-01-17 11:57:00 +0900
categories: [백준, 백준 알고리즘 강의 문제 시리즈]
tags: [devrunner, BOJ, C++, 백준, 알고리즘 기초 1, 자료구조, 스택, BOJ 17413]
---

## 링크

---

<https://www.acmicpc.net/problem/17413>

## 문제 접근 방법

---

[시리즈 2편](https://baejw0111.github.io/posts/BOJ-series-2-9093/)에서 풀었던 [단어 뒤집기](https://www.acmicpc.net/problem/9093) 문제의 후속 문제이다.

전 문제와 알고리즘은 같지만 다른 점이 2가지가 있다.

1. 문자열을 하나만 받는다.
2. `<>` 안의 문자들의 순서는 바꾸지 않는다.

- 꺽쇠 기호가 나왔는지 여부를 나타내는 `bracket`이란 변수를 두어 '<'기호가 나올 시 `bracket`을 `1`로 두고, 해당 상태일 때 단어 뒤집기를 시행하지 않는다.
  반대로 '>'가 나올 시 `bracket`을 다시 `0`으로 바꿔준다.

- <span style="color:red">주의할 점</span>이 있는데, 공백을 포함한 문자열을 입력 받아야 하기 때문에 제대로 입력받으려면 `getline`함수를 써야 한다.

## 코드

---

<details>
<summary>펼치기</summary>
<div markdown="1">

```cpp
#include <bits/stdc++.h>
using namespace std;

// 단어 전용 스택
stack<char> word;
// 꺽쇠 기호 존재 상태
int bracket = 0;

// word를 비우면서 출력하는 함수
void clear() {
  while (!word.empty()) {
    cout << word.top();
    word.pop();
  }
}

int main() {
  ios_base::sync_with_stdio(false);
  cin.tie(NULL);
  cout.tie(NULL);
  // c++의 표준 stream의 동기화를 끊는 역할을 하여 입출력의 속도를 높인다.

  string S;

  getline(cin, S);

  for (char a : S) {
    if (!bracket) {
      if (a == ' ' || a == '<') {
        clear();
        cout << a;
      } else {
        word.push(a);
      }
    } else {
      cout << a;
    }

    if (a == '<') {
      bracket = 1;
      continue;
    } else if (a == '>') {
      bracket = 0;
    }
  }

  clear();

  return 0;
}
```

</div>
</details>

## 인증

---

![image](https://user-images.githubusercontent.com/87963766/212794566-665a2053-29f3-406f-9165-e8df236f9327.png)
