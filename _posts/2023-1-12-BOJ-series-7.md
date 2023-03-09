---
title: "[백준 알고리즘 강의 문제 시리즈 - 7] 1158번 : 요세푸스 문제"
date: 2023-01-12 11:01:00 +0900
categories: [백준,백준 알고리즘 강의 문제 시리즈]
tags: [devrunner,BOJ,C++,백준,알고리즘 기초 1,자료구조,큐,1158]
---

링크
---
<https://www.acmicpc.net/problem/1158>
<br/><br/>


문제 접근 방법
---
* 컴공과 자료구조 시간에 원형큐 배울 때 나오는 문제인 요세푸스 문제이다.
<br/><br/>

* 이 문제는 굳이 원형 구조의 자료구조를 구현하지 않고도 선입선출(FIFO) 구조인 STL에 구현된 큐를 이용하여 쉽게 풀 수 있다.

> 1. 순서가 다음으로 넘어갈 때마다 `order` 변수에 1씩 더해주며 해당 수가 k로 나누어 떨어질 때마다 해당 순서의 번호를 제거 후 출력한다.
> 2. 그 외의 경우는 다시 큐에 넣어준다.

* 위의 두 과정을 큐가 비어있는 상태가 될 때까지 반복한다.
<br/><br/>

이번 문제는 STL을 사용한 코드와 예전에 STL을 안 쓰고 원형 연결리스트를 따로 구현한 코드까지 첨부했다. 예전에 썼던 코드가 아깝기도 하고, STL을 사용하면 코드 작성이 얼마나 용이해지는 지 한 번 보여주고 싶었다. 개발자에게 있어서 코드 라인 수를 줄이는 것은 상당히 중요한 일이니 말이다.
<br/><br/>

![image](https://user-images.githubusercontent.com/87963766/211946409-44d24261-3cab-4813-b87e-386f276361bc.png)
###### <center>컴퓨터를 다루는 사람이라면 이런 사람이 되지 말자.<center>
<br/><br/>

원형 연결리스트 직접 구현해서 사용한 코드
---
<details>
<summary>펼치기</summary>
<div markdown="1">

```cpp
#include <iostream>
using namespace std;

class CDLL{
    struct node{
        int num;
        node *prev,*next;
    };
    using link=node*;

    link head;

public:
    CDLL();
    void Add(int x);
    void Delete(int x);
    int Empty();
    void Josephus(int n,int k);
    void Display();
    ~CDLL();
};

int main(){
    int n,k;
    cin>>n>>k;

    CDLL ring;

    for(int i=1;i<=n;i++){
        ring.Add(i);
    }

    ring.Josephus(n,k);

    return 0;
}

CDLL::CDLL():head(new node){
    head->prev=head;
    head->next=head;
}

void CDLL::Add(int x){
    link tmp=new node;
    tmp->num=x;

    if(Empty()){
        tmp->next=tmp;
        tmp->prev=tmp;

        head->next=tmp;
    }
    else{
        tmp->prev=head->next->prev;
        tmp->next=head->next;

        head->next->prev->next=tmp;
        head->next->prev=tmp;
    }
}

void CDLL::Delete(int x){
    if(Empty()){
        return;
    }

    link i=head->next;
    do{
        if(i->num==x){
            if(i==head->next){
                if(head->next->next==head->next){
                    head->next=head;
                }
                else{
                    head->next=i->next;
                }
            }
            i->prev->next=i->next;
            i->next->prev=i->prev;
            delete i;
            return;
        }

        i=i->next;
    }while(i!=head->next);

}

int CDLL::Empty(){
    if(head->next==head){
        return 1;
    }
    else{
        return 0;
    }

}

void CDLL::Josephus(int n,int k){
    int order=0;
    link cur=head;

    cout<<"<";

    while(!Empty()){
        cur=cur->next;
        order+=1;

        if(order==k){
            order=0;
            cur=cur->prev;
            cout<<cur->next->num;
            Delete(cur->next->num);
            if(Empty()){
                cout<<">";
            }
            else{
                cout<<", ";
            }
        }

    }
    cout<<endl;
}

void CDLL::Display(){
    link tmp=head->next;

    do{
        cout<<tmp->num<<" ";
        tmp=tmp->next;
    }while(tmp!=head->next);
    cout<<endl;
}

CDLL::~CDLL(){
    head->next->prev->next=NULL;

    while(head){
        link tmp=head;
        head=head->next;
        delete tmp;
    }
}
```

</div>
</details>
<br/><br/>

STL에 구현된 큐를 사용한 코드
---
<details>
<summary>펼치기</summary>
<div markdown="1">

```cpp
#include <iostream>
#include <queue>
using namespace std;

int n,k;

void Josephus(){
    queue<int> ring;
    //순서
    int order=1;

    //1부터 n까지 큐에 넣기
    for(int i=1;i<=n;++i){
        ring.push(i);
    }

    cout<<'<';
    while(!ring.empty()){
        //큐의 가장 앞 원소를 임시 변수에 저장
        int tmp=ring.front();

        ring.pop();

        //k번째 번호 제거 후 출력
        if(order%k==0){
            cout<<tmp;
            if(!ring.empty()){
                cout<<", ";
            }
        }
        else{
            ring.push(tmp);
        }

        order++;
    }

    cout<<'>';
}

int main(){
    cin>>n>>k;

    Josephus();

    return 0;
}
```

</div>
</details>
<br/><br/>

인증
---
![image](https://user-images.githubusercontent.com/87963766/211957241-79a4439a-2aa8-4130-8222-a5f990804aec.png)
