---
title: "[리눅스 - 쉘 프로그래밍] 3. 사용자와 파일 권한"
date: 2023-04-08 09:00:00 +0900
categories: [임베디드, 리눅스]
tags: [devrunner, imbedded, linux, shell programming, linux file system]
---

## **Host**

---

### **리눅스와 Host**

리눅스는 한 컴퓨터를 여러 명이 사용하는 **다중 사용자 시스템**으로 설계 되었다.

**Host**는 네트워크에 연결된 이 한 대의 컴퓨터를 의미한다.

![image](https://user-images.githubusercontent.com/87963766/227756821-122504e2-54e7-4f25-85d5-0430a1351c64.png)

위 사진처럼 리눅스 터미널을 열면 `(user name)@(host name)`의 형식으로 표시된다.

### **사용자 계정 관리**

- `sudo su`: 사용자 변경

- `exit`: 원래 유저로 돌아옴

- `adduser (계정명)`: 계정 생성

- `deluser (계정명)`: 계정 삭제

  - `--remove-all-files`: 계정의 모든 파일 다 삭제

## **그룹**

---

권한을 단체 설정하기 위해 리눅스에서는 **Group** 단위로 계정들을 관리한다.

- `groups (계정명)`: 해당 계정의 소속 그룹 확인

- `addgroup (그룹명)`: 그룹 생성 -`gpasswd`: 그룹에 계정 추가 및 제거

  - `-a (계정명) (그룹명)`: 그룹에 계정 추가(add)

  - `-d (계정명) (그룹명)`: 그룹에 계정 제거(delete)

유저는 여러 그룹에 소속되는 것이 가능하다.

- `cat /etc/group | grep (그룹명)`: 각 그룹에 누가 소속되어 있는지 확인

- `delgroup (그룹명)`: 그룹 삭제

## **파일 권한 설정**

---

### **파일 종류**

리눅스에서는 파일과 폴더(디렉토리)를 **모두 똑같이 파일로 취급**한다.
리눅스에서 관리하는 파일 종류는 다음과 같다

- **Reguler** File: 일반 파일
- **Directory** File: 폴더
- **Link** File: 바로가기 파일
- **Device** File: 장치 제어 파일

### **권한**

`ls -al` 입력 시 다음과 같이 표시된다.

|                   |           |      |           |           |                     |           |
| :---------------: | :-------: | :--: | :-------: | :-------: | :-----------------: | :-------: |
| 파일 종류 및 권한 | 링크 개수 | 오너 | 오너 그룹 | 파일 크기 | 파일 최종 수정 일시 | 파일 이름 |

- 예시:

  ```
  drwxr-xr-x  2 bjw011 bjw011 4096  3월 20 22:41 템플릿
  ```

<br>

여기서 `파일 종류 및 권한`은 다음과 같은 순서로 표시된다.

|           |                         |                              |                          |
| :-------: | :---------------------: | :--------------------------: | :----------------------: |
| 파일 종류 | 오너의 파일에 대한 권한 | 오너 그룹의 파일에 대한 권한 | Ohter의 파일에 대한 권한 |

여기서 `Ohter`는 오너와 오너 그룹이 아닌 유저를 의미한다.
<br>

- 파일 종류

  - `-`: Reguler File

  - `d`: Directory File

  - `l`: Link File

  - `c`,`b`: Device File

- 파일 권한(권한이 없을 경우 `-`로 표시됨)

  - `r`: 읽기(read) 권한

  - `w`: 쓰기(write) 권한

  - `x`: 실행(execution) 권한

### **파일 정보 변경**

`sudo chown (계정명):(그룹명) (파일명)`: **Ch**ange **Own**er.
파일의 Owner(user)와 Group 변경

`chmod (모드) (파일명)`: **Ch**ange **mod**e.
각각에 주어진 파일의 권한을 "**File Mode**"라고 하는데, 이 명령어는 이걸 바꾸는 명령어다.

다양한 설정법이 있다.

- 예시

  ```bash
  # **user를 rwx로 바꾸기**
  ---
  $sudo chmod u=rwx ./aaa

  # **group를 rw-로 바꾸기**
  ---
  $sudo chmod g=rw- ./bbb

  # **other를 r-x로 바꾸기**
  ---
  $sudo chmod o=rx ./ccc

  # **----------------------**
  ---

  # **수식 이용**
  ---

  # **user에 r권한 추가**
  ---
  $sudo chmod u+r ./aaa

  # **other에 r권한 제외**
  ---
  $sudo chmod o-r ./bbb

  # **u,g,o 모두 w 권한 추가(a는 all을 의미)**
  ---
  $sudo chmod a+w ./aaa

  # **----------------------**
  ---

  # **2진수 환산**
  ---

  # **--x--x-rw = 113**
  ---
  # **rwxrwxrwx = 777**
  ---
  # **rw-rw----= 660**
  ---

  $sudo chmod 113 ./aaa
  $sudo chmod 777 ./bbb
  $sudo chmod 660 ./ccc
  ```

### \***\*\*참고 1**) 실행 파일의 권한\*\*

따라서 텍스트 파일을 실행하려면 `u=rx`로 권한 설정을 따로 해야한다.

### \***\*\*참고 2**) 디렉토리의 권한\*\*

- read: `ls`로 파일 목록을 읽을 수 있는 권한
