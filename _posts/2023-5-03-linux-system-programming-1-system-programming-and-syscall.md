---
title: "[리눅스 - 시스템 프로그래밍] 1. 시스템 프로그래밍, System Call"
date: 2023-05-03 17:27:00 +0900
categories: [임베디드, 리눅스]
tags: [devrunner, imbedded, linux, system programming, syscall]
---

## **주요 용어 정리**

---

### **컴퓨팅 시스템**

CPU, 기억장치 , 입출력장치 등이 상호작용을 하는 집합체다.

### **임베디드 시스템**

컴퓨팅 시스템 중 전용 기능을 수행하도록 만들어진 시스템으로, PC와 달리 특정 목적을 가진다.

### **Peripheral**

컴퓨팅 시스템의 하드웨어에서, CPU와 메모리를 제외한 주변 장치들을 의미한다.
모니터와 키보드 같은 입출력장치나 LAN 카드, 그래픽 카드 등이 이에 해당한다.

### **Middleware**

API, Library와 같이 서로 다른 애플리케이션이 서로 통신하는 데 사용되는 중간 단계의 소프트웨어를 의미한다.

### **POSIX**

---

POSIX는 **IEEE가 제정한 유닉스의 API의 표준 규격**이다.

App 개발자들은 App을 개발하려면 OS가 제공하는 API를 알아야한다.
문제는 세상에는 여러 OS들이 존재하고, OS마다 API가 다르다는 점이다.

이런 문제를 해결하기 위해 OS마다 제공되는 API들을 하나로 통일한 것이 바로 **POSIX**다.

리눅스 또한 이 규격을 따른다.

## **파일 처리 System Call(Low Level API)**

---

### **System Call이란?**

System Call은 **리눅스 App이 리눅스 커널에 명령을 내리기 위해 만들어진 API**다.
즉 커널 레벨에서 동작하는 Low Level API다.
줄여서 **Syscall**이라고도 한다.

C언어의 `printf`, `scanf`, `fopen`과 같은 표준 입출력 함수(High Level API)들이 이 System Call로 만들어졌다.

임베디드 시스템에서 장치 제어를 위해서는 장치 파일(Device File)을 읽어야 한다.
이를 위해서는 파일 처리 System Call이 필수적이다.

장치 파일은 Low Level API를 써야만 읽을 수 있기 때문이다.

다음은 주요 syscall들을 정리해놓은 내용들이다.

### **`open`**

- 역할

  `pathname`의 파일을 연다.

  - 예시

    ```c
    int fd = open("./test.txt", O_RDONLY, 0);
    ```

- 필수 헤더

  ```c
  #include <sys/types.h>
  #include <sys/stat.h>
  #include <fcntl.h>
  ```

- 원형

  ```c
  open(const char *pathname, int flags, mode_t mode);
  ```

- File Descriptor

  프로그램에서 open 함수를 실행해 파일에 접근하려고 할 때 사용되는 파일에 부여되는 정수가 반환된다.

- flag

  - 필수 옵션

    - `O_RDONLY`: 읽기만 가능

    - `O_WRONLY`: 쓰기만 가능

    - `O_RDWR`: 읽기 쓰기 모두 가능

  - 추가 옵션('`|`' 연산으로 추가)

    - `O_CREAT`: 없으면 새로 생성

    - `O_APPEND`: 덧붙이기

    - `O_TRUNC`: 파일 내용 제거 후 사용

- mode

  - 파일이 없어 새로 생성하는 경우에 해당 파일의 권한을 8진수 값으로(0xxx) 부여한다.

    - 예1) 0777: rwxrwxrwx

    - 예2) 0644: rw-r--r--

  - 단순히 파일을 열 때는 해당 옵션이 필요없기 때문에 0을 넣는다.

- 유의사항

  fd가 음수일 경우 에러를 뜻한다.
  open 함수는 에러가 잦기 때문에 다음과 같이 에러가 발생할 경우에 로그 메세지를 출력하도록 것이 좋다.

  ```c
  int fd = open("./test.txt", O_RDONLY, 0644);
  if (fd < 0) {
    printf("FILE OPEN ERROR\n");
    exit(1);
  }
  ```

  다음과 같이 매크로를 이용해 에러가 발생한 위치를 확인할 수도 있다.

  ```c
  // __FILE__: 에러 file 이름
  // __LINE__: 에러 line 번호

  if(fd < 0){
    printf("[%s :: %d] FILE OPEN ERROR\n", __FILE__, __LINE__);
    exit(1);
  }
  ```

### **`close`**

- 역할

  file descriptor(fd)에 할당된 파일을 닫는다.

- 필수 헤더

  ```c
  #include <unistd.h>
  ```

- 원형

  ```c
  int close(int fd);
  ```

### **`write`**

- 역할

  file descriptor(fd)에 할당된 파일에 buf의 내용을 count byte만큼 쓴다.

  - 예시

    ```c
    int fd = open("./test.txt", O_WRONLY | O_TRUNC, 0664);
    char buf[100] = "My name is BJW";
    write(fd, buf, strlen(buf));
    ```

- 필수 헤더

  ```c
  #include <unistd.h>
  ```

- 원형

  ```c
  ssize_t write(int fd, const void *buf, size_t count);
  ```

### **`read`**

- 역할

  file descriptor(fd)에 할당된 파일을 count byte만큼 읽어와 buf에 담는다.

  - 예시

    ```c
    int fd = open("./test.txt", O_WRONLY | O_TRUNC, 0664);
    char buf[100] = "My name is BJW";
    write(fd, buf, strlen(buf));
    ```

- 필수 헤더

  ```c
  #include <unistd.h>
  ```

- 원형

  ```c
  ssize_t read(int fd, void *buf, size_t count);
  ```

- offset

  read 수행 시, 어디까지 읽었는지가 내부적으로 저장된다.
  이를 나타내는 값이 offset이다.

### **`lseek`**

- 역할

  기준점(`whence`)에서 `offset`만큼 떨어져 있는 곳으로 파일 offset을 옮긴다.

- 필수 헤더

  ```c
  #include <sys/types.h>
  #include <unistd.h>
  ```

- 원형

  ```c
  off_t lseek(int fd, off_t offset, int whence);
  ```

- whence

  - `SEEK_CUR`: 현재 위치

  - `SEEK_SET`: 시작점

  - `SEEK_END`: 끝

## **표준 입출력과 Low Level API의 차이**

---

### **표준 입출력(High Level API)**

- `fopen`, `fseek`, `fclose` 등

- 사용하기 쉽고 , 기능이 많다.

- 개발속도가 빠르다.

- Low Level 명령어를 Wrapping한 함수다.

### **Low Level API**

- `open`, `write`, `lseek` 등

- 쓰기 불편하다.

- 하지만 임베디드에서 Device File을 다룰 때 필수적이다.
