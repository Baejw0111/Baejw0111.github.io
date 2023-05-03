---
title: "[리눅스 - 시스템 프로그래밍] 1. 시스템 프로그래밍, System Call"
date: 2023-05-03 17:40:00 +0900
categories: [임베디드, 리눅스]
tags: [devrunner, imbedded, linux, system programming, thread]
---

## **멀티태스킹과 Thread**

---

**한 프로세스 내에서** 여러 작업을 동시 실행하기 위해 필요한 것이 바로 **Thread**이다.
이를 사용하려면 운영체제가 API로 지원해줘야 하는데, 이를 위해 Thread POSIX API가 존재한다.

## **void \***

---

POSIX Thread API에서 `void*`를 사용하기 때문에, 이게 뭔지 먼저 알아야 한다.

void 포인터는 **어떤 타입의 주소도 모두 다 저장할 수 있는 포인터**이다.
그냥 귀찮으면 `void*` 변수를 선언하고 여기에 아무 포인터나 집어넣으면 된다.

**하지만 주소를 저장만 할 수 있을 뿐, 사용할 수는 없다.**
즉, 다음과 같이 코드를 짜면 에러가 난다.

```c
int a = 1;

void* p = &a;

printf("%d", *p); // <--- 여기서 에러가 난다.
```

그래서 다음과 같이 포인터 값을 넘겨야 할 경우에 사용되며, 형변환을 한 후 사용되곤 한다.

```c
#include <stdio.h>

void abc(void *v) {
  int *p = (int *)v;
  printf("%d", *p);
}

int main() {
  int x = 10;

  abc(&x);

  return 0;
}
```

## **Thread Programming**

---

Thread 프로그래밍 시 **pthread Library**를 사용하기 때문에 해당 라이브러리를 링크해줘야 한다.
빌드 시 링크 옵션으로 다음 예시처럼 `-lpthread`를 넣어주자.

```bash
$gcc ./thread.c -o ./thread -lpthread
```

당연히 헤더파일은 `pthread.h`를 include해줘야 한다.

그리고 Thread API는 인자로 `void*`를 받기 때문에 사용할 Thread 함수는 다음과 같이 `void*`를 리턴하는 형태로 짜야 한다.
또한 리턴값은 생략할 수 있다.

```c
void *abc(){

}
```

다음은 주요 pthread 함수들이다.

### **`pthread_create`**

- 역할

  스레드를 생성한다.

  - 예시

    ```c
    pthread_t t;

    pthread_create(&t, NULL, func, NULL);
    ```

- 원형

  ```c
  int pthread_create(pthread_t *thread, const pthread_attr_t *attr,
                      void *(*start_routine) (void *), void *arg);
  ```

- argument

  - `thread`: thread id 저장될 변수 주소

  - `attr`: 스레드 설정(기본값은 NULL)

  - `start_routine`: 실행할 함수 이름

  - `arg`: 함수에 전달할 인자값(여러 값 넘기고 싶은 경우 구조체 사용)

### **`pthread_join`**

- 역할

  `phtread_create`로 인해 생성된 스레드가 `pthread_join`을 만나면 스레드가 종료되며, 이후 커널 내부 정리 작업(메모리 해제)이 진행된다.
  `open` 이후에 `close`를 반드시 써야하는 것처럼, 스레드 사용 시 반드시 써야하는 함수다.

- 원형

  ```c
  int pthread_join(pthread_t thread, void **retval);
  ```

- argument

  - `thread`: thread id 저장될 변수 주소

  - `retval`: NULL이 아닐 경우 대상 스레드의 종료 상태를 retval이 가리키는 위치로 복사한다.

### **`pthread_self`**

- 역할

  해당 스레드의 thread id값을 얻을 수 있다.
  참고로 `pthread_t`의 자료형은 `unsigned long int`다.

  - 예시

    코드:

    ```c
    #include <pthread.h>
    #include <stdio.h>
    #include <stdlib.h>

    void *abc() {
      pthread_t id = pthread_self();
      printf("[%lu] \n", id);
    }

    int main() {
      pthread_t tid[4];

      for (int i = 0; i < 3; ++i) {
        pthread_create(&tid[i], NULL, abc, NULL);
        printf("%lu\n", tid[i]);
      }

      for (int i = 0; i < 3; ++i) {
        pthread_join(tid[i], NULL);
      }

      return 0;
    }
    ```

    결과:

    ```
    140632147851008
    140632139458304
    140632131065600
    [140632131065600]
    [140632147851008]
    [140632139458304]
    ```

- 원형

  ```c
  pthread_t pthread_self(void);
  ```

### **\*참고\*\*) `thread.h`와 `pthread.h`의 차이**

그런데 임베디드에서는 `pthread.h`를 쓰는데, 둘이 무슨 차이일까?

둘의 가장 큰 차이점은 **POSIX 표준을 얼마나 지키고 있는지**에 있다.

`thread.h`의 경우 GNU C 라이브러리에서의 스레드 구현에만 치중되어 POSIX 표준을 완전히 구현되지 않은 반면, `pthread.h`에는 POSIX 표준이 완전히 구현되어있다.
또한, `pthread.h`가 `thread.h`에 비해 고급 기능을 더 제공한다는 것도 큰 차이점이다.

따라서 임베디드 시스템에서는 `pthread.h`를 사용하는 것이 좋다.

## **공유 자원과 동기화**

---

### **메모리 공유로 인해 발생하는 문제들**

동시에 실행되고 있는 스레드들이 한 자원을 참조하게 되면 예상치 못한 결과가 발생하게 된다.
이러한 메모리 공유로 인해 발생되는 문제를 다루기 위해 다음과 같은 것들을 고려해야 한다.

- Race condition: Thread 또는 Process의 타이밍에 따라 결과 값이 달라질 수 있는 상태

- Critical Section: Thread 또는 Process가 동시에 접근하면 안되는 부분

### **동기화**

위 문제들을 해결하려면 스레드 간에 동기화가 이뤄져야한다.
동기화를 하기 위한 방법으로는 다음과 같은 방법들이 있다.

- `pthread.h`의 동기화 알고리즘 사용

  다음과 같은 알고리즘들이 있다.

  - Mutex

  - Semaphore

  - Spin Lock

  - Barrier

- `sleep`이용하기

  `sleep`으로 함수가 실행되는동안 다른 스레드의 실행을 멈춘다.
  하지만 이 방법의 경우 함수의 실행시간이 길면 전체 프로그램의 성능이 하락할 수 있다.

- `mutex_lock` 객체 사용
  각 스레드에게 공유자원을 사용할 수 있는 권한을 주어 동시 사용을 막는 방법이다.

## **mutex**

---

다음은 주요 mutex 함수들이다.

### **`pthread_mutex_init`**

- 역할

  mutex 객체를 초기화 한다.

- 원형

  ```c
  int pthread_mutex_init(pthread_mutex_t *__mutex, const pthread_mutexattr_t *__mutexattr)
  ```

- argument

  - `mutex`: 초기화 할 mutex 객체

  - `mutexattr`: mutex 객체의 속성을 주는 인자로, 기본적으로는 NULL을 넣는다.

### **`pthread_mutex_destroy`**

- 역할

  mutex 객체를 제거한다.

- 원형

  ```c
  int pthread_mutex_destroy(pthread_mutex_t *__mutex)
  ```

### **`pthread_mutex_lock`**

- 역할

  mutex lock을 요청하여 얻는다.
  얻지 못하는 경우 얻을 때까지 해당 스레드는 block된다.

- 원형

  ```c
  int pthread_mutex_lock(pthread_mutex_t *__mutex)
  ```

### **사용 예시**

```c
#include <pthread.h>
#include <stdio.h>
#include <unistd.h>

pthread_mutex_t mlock;
pthread_t t[4];
int cnt;

void *run() {
  pthread_mutex_lock(&mlock);

  for (int i = 0; i < 10000; ++i)
    ++cnt;

  pthread_mutex_unlock(&mlock);
}

int main() {
  pthread_mutex_init(&mlock, NULL);

  for (int i = 0; i < 4; ++i) {
    pthread_create(&t[i], NULL, run, NULL);
  }

  for (int i = 0; i < 4; ++i) {
    pthread_join(t[i], NULL);
  }

  printf("%d\n", cnt);

  return 0;
}
```
