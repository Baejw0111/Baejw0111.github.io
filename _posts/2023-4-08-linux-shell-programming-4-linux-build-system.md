---
title: "[리눅스 - 쉘 프로그래밍] 4. 빌드 시스템"
date: 2023-04-08 09:00:00 +0900
categories: [임베디드, 리눅스]
tags:
  [
    devrunner,
    imbedded,
    linux,
    shell programming,
    linux build system,
    make,
    Makefile,
    CMake,
  ]
---

## **gcc**

---

### **gcc 빌드 과정**

gcc의 빌드 과정은 다음 두 과정으로 이뤄진다.

1. compile & assemble

2. Linking

### **빌드 명령어**

- `-c`: C 파일 컴파일 및 assemble

- `-o`: Object 파일들과 라이브러리 함수들을 하나로 합쳐(linking) output 파일의 이름을 따로 지정한다.
  (이 옵션을 안쓰고 그냥 링킹하면 `out`확장자 파일이 생성된다.
  `-o` 옵션을 사용해 만든 파일과 같은 기능을 하는 파일이다.)

- 예시

  ```bash
  $gcc -c ./ blue.c
  $gcc -c ./ pink.c
  $gcc -c ./ main.c
  $gcc ./main.o ./blue.o ./pink.o -o ./bluepink
  $rm -r ./*.o
  ```

## **make 빌드 시스템**

---

빌드 스크립트 만들 때 python이나 bash shell 스크립트를 사용하면 쓸데없는 작업을 하게 되어 빌드 시간이 오래 걸리게 된다.
이를 위해 **make 빌드 시스템**을 사용한다.

"Makefile"이란 스크립트 파일을 만들어 빌드 과정을 작성한다.

- 예시

  ```make
  bluepink: blue.o pink.o main.o
  	gcc blue.o pink.o main.o -o bluepink

  blue.o: blue.c
  	gcc -c blue.c

  pink.o: pink.c
  	gcc -c pink.c

  main.o: main.c
  	gcc -c main.c
  ```

### **장점**

- 빌드 자동화

- 빌드 속도 최적화로 불필요한 과정 생략이 가능하다.

예를 들어, 빌드 해야 할 C 파일들 중 한 파일에서만 수정이 이뤄졌을 경우, 전체를 다시 빌드하지 않고, 해당 파일에 대해서만 다시 빌드를 한다.

### **CMake**

CMake는 Makefile을 자동 생성을 할 수 있는 빌드 시스템이다.
**CMakeLists.txt** 파일을 만들어 작성한다.

- 예시

  ```CMake
  ADD_EXECUTABLE(gogo main.c blue.c pink.c)
  ```

아래의 명령으로 Makefile을 자동 생성할 수 있다.

```bash
$cmake .
```

## **make 스크립트 문법**

---

사실 CMake를 쓰면 Makefile을 알아서 만들 수 있지만, 실무에서 Makefile을 직접 읽고 편집해야 할 상황이 생길 수 있기에 make 스크립트 문법을 알아놓는 것이 좋다.

### **구성요소**

타겟과 쉘 명령어로 이루어진다.

- 예시

  ```make
  HI:
  	echo "hi"
  ```

  출력 결과:

  ```
  echo "hi"
  hi
  ```

### **명령어 출력 생략**

쉘 명령어 앞에 `@` 추가 시 명령어 출력을 생략한다.

- 예시

  ```make
  HI:
  	@echo "hi"
  ```

  출력 결과:

  ```
  hi
  ```

### **의존성 타겟**

타겟 별로 타겟 실행 시에 필요한 요소인 **의존성 타겟**을 설정을 할 수 있다.
의존성 타겟으로 다른 **타겟**을 설정할 수도 있고, 현재 디렉토리 내에 존재하는 **파일**을 설정할 수도 있다.

- 예시

  ```make
  HI: one
  	@echo "hi"

  one:
  	@echo "one"
  ```

  출력 결과:

  ```
  one
  hi
  ```

### **매크로 선언**

- 선언: Makefile을 컴퓨터가 분석할 때 매크로에 대해서 먼저 전체적으로 처리를 하고 실행을 하기 때문에, 매크로에 매크로의 선언이나 연산하는 위치는 어디서 해도 스크립트 순서에 구애받지 않는다.
  하지만 가독성을 위해 최상단에 적는 것이 좋다.

- 정의: 매크로는 C에서 변수를 정의하는 것처럼 정의한다.

- 치환: `$()`또는 `${}`로 치환이 가능하다.
  둘 중에 아무거나 써도 상관 없지만 `$()`로 통일시키는 편이 낫다.
  또한 정의되지 않은 변수는 빈칸으로 치환된다.

- 수정: `+=`기호로 매크로 내용을 추가할 수 있다.
  타겟 정의 후에 매크로 내용을 추가해도 앞서 말한 것 때문에 실행 시 최종 결과값이 출력된다.

- 예시

  ```make
  MSG1 = "One"
  MSG2 = "Two"

  HI: one two
  	@echo "Hi"

  HELLO:
  	@echo ${asdasd}

  one: HELLO
  	@echo $(MSG1)

  two:
  	@echo ${MSG2}

  MSG2 += "Three"
  ```

  출력 결과:

  ```

  One
  Two Three
  Hi
  ```

### **매크로 대입 연산자**

- `:=`(Simple Equal): 스크립트 순서대로 현재 기준에서 값을 대입한다.

- `=`(Reculsive Equal): 스크립트 전체 실행 후의 최종 값을 대입한다.

- 예시

  ```make
  NAME = "OH"

  SIMPLE := $(NAME)
  RECUL = $(NAME)

  NAME += "GOOD"
  NAME += "KFC"

  who:
  	@echo $(SIMPLE)
  	@echo $(RECUL)
  ```

  출력 결과:

  ```
  OH
  OH GOOD KFC
  ```

### **주석**

주석은 파이썬처럼 행 앞에 `#`를 붙이면 된다.

### **내부 매크로**

- `$@`: 타겟의 이름으로 치환된다.

- `$^`: 타겟의 의존성 타겟들로 치환된다.

- `$<`: 의존성 타겟 중 첫번째 타겟으로 치환된다.

- 예시

  ```make
  CC = gcc

  go: go.o hi.o
  	$(CC) -o $@ $^
  	rm ./*.o

  go.o: go.c
  	$(CC) -c $^

  hi.o: hi.c
  	$(CC) -c $^
  ```

  출력 결과:

  ```
  gcc -c go.c
  gcc -c hi.c
  gcc -o go go.o hi.o
  rm ./*.o
  ```
