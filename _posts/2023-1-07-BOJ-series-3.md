---
title: "[백준 알고리즘 강의 문제 시리즈 - 3] 9012번 : 괄호"
date: 2023-01-09 09:24:00 +0900
categories: [백준,백준 알고리즘 강의 문제 시리즈]
tags: [devrunner,BOJ,C++,백준,알고리즘 기초 1,자료구조,스택,9012]
---

링크
---
<https://www.acmicpc.net/problem/9012>
<br/><br/>


문제 접근 방법
---
1. 모든 괄호가 서로 짝이 있는지(VPS) 아닌지를 판단하는 문제이다.<br/><br/>
2. 문자열을 스캔하면서 왼쪽 괄호가 나오면 스택에 Push하고 오른쪽 괄호가 나오면 Pop을 하면 된다.<br/><br/>
3. 과정이 종료됐을 때 스택이 비어있다면 YES, 비어있지 않다면 NO를 출력하면 된다.
<br/><br/>

코드
---
```cpp
#include <iostream>
#include <string>
using namespace std;

template <typename T>
class Stack{
    struct node{
        T num;
        node* next;
    };
    using link=node*;

    link top;

public:
    Stack():top(NULL){}
    void Push(T x);
    int Pop();
    int Empty();
    ~Stack();
};

void VPS(string str){
    Stack<char> stk;

    for(int i=0;i<str.length();i++){
        if(str[i]=='('){
            stk.Push(str[i]);
        }
        else{
            if(stk.Pop()==0){
                cout<<"NO"<<'\n';
                return;
            }
            else{
                continue;
            }
        }
    }

    if(stk.Empty()==1){
        cout<<"YES"<<'\n';
    }
    else{
        cout<<"NO"<<'\n';
    }
}

int main(){
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);
    //c++의 표준 stream의 동기화를 끊는 역할을 하여 입출력의 속도를 높인다.

    int n;
    cin>>n;
    cin.ignore();

    for(int i=0;i<n;i++){
        string str;
        getline(cin,str);

        VPS(str);
    }


    return 0;
}


template <typename T>
void Stack<T>::Push(T x){
    if(top==NULL){
        top=new node;
        top->num=x;
        top->next=NULL;
    }
    else{
        link tmp=new node;
        tmp->num=x;
        tmp->next=top;
        top=tmp;
    }
}

template <typename T>
int Stack<T>::Pop(){
    if(top==NULL){
        return 0;
    }
    else{
        top=top->next;
        return 1;
    }
}

template <typename T>
int Stack<T>::Empty(){
    if(top==NULL){
        return 1;
    }
    else{
        return 0;
    }
}

template <typename T>
Stack<T>::~Stack(){
    while(top){
        link tmp=top;
        top=top->next;
        delete tmp;
    }
}
```

인증
---
![image](https://user-images.githubusercontent.com/87963766/211226661-10f41ff2-b9fe-420f-a208-9c06aba3b49b.png)
