# Race Condition (경쟁 조건)

> 2개 이상의 프로세스가 공유 자원을 병행적으로 읽거나 쓰는 상황을 경쟁 조건이 발생했다고 한다
> 

### 상호 배제(Mutual exclusion)

- Race condition을 막기 위해서는 두 개 이상의 프로세스가 공용 데이터에 동시에 접근을 하는 것을 막아야 한다
- 즉, 한 프로세스가 공용 데이터를 사용하고 있으면 그 자원을 사용하지 못하도록 막거나, 다른 프로세스가 그 자원을 사용하지 못하도록 막으면 이 문제를 피할 수 있다
    - 상호 배제라고 부름

### 교착 상태(Deadlock)

- 상호 배제를 시행하면 추가적인 제어 문제가 발생
- 하나가 교착 상태
- 프로세스가 각자 프로그램을 실행하기 위해 두 자원 모두에 엑세스 해야 한다고 가정할 때 프로세스는 두 자원 모두를 필요로 하므로 필요한 두 리소스를 사용하여 프로그램을 수행할 때까지 이미 소유한 리소스를 해제하지 않는다
- 이러한 상황에서 두 프로세스는 교착 상태에 빠지게 되는 문제가 발생할 수 있다

### 기아 상태(Starvation)

- 프로세스들이 더 이상 진행을 하지 못하고 영구적으로 블록되어 있는 상태
- 시스템 자원에 대한 경쟁 도중에 발생할 수 있고 프로세스 간의 통신 과정에도 발생할 수 있는 문제
- 두 개 이상의 작업이 서로 상대방의 작업이 끝나기만을 기다리고 있기 때문에 결과적으로는 아무것도 완료되지 못하는 상태가 됨

- 경쟁 조건에서는 스레드의 실행 순서를 잘 조절해주지 않으면 비정상적인 상태가 나오게 된다
- 이 문제는 항상 발생하느 것이 아니라 특정한 순서대로 수행되었을 때 발생
- 이러한 문제가 발생하지 않도록, 운영체제는 다른 프로세스의 의도하지 않은 간섭으로부터 각 프로세스의 데이터 및 물리적 자원을 보호해야 하며 여기에 메모리, 파일 및 I/O 장치와 관련된 내용이 포함
- 프로세스에서 수행하는 내용과 프로세스가 생성하는 결과는, 다른 동시 프로세스의 실행 속도와 무관, 즉 기능과 결과는 서로 독립적이어야 한다.

## 예방

### 세마 포어

![img1.daumcdn.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcgvF68%2FbtqDyMXcTWu%2FzhuMLl9YWBrhRkv6xkEm11%2Fimg.png)

- 공유된 자원의 데이터를 여러 프로세스가 접근하는 것을 막는 방법
- 일반적으로 비교적 긴 시간을 확보하는 리소스에 대해 이용하게 되며, 운영체제의 리소스를 경쟁적으로 사용하는 다중 프로세스에서 행동을 조정하거나 동기화 시키는 기술

### 뮤텍스

![img1.daumcdn.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FKK4GG%2FbtqDyMXcTVK%2FdMLkVA1QUmN3khbdFuxoF1%2Fimg.png)

- 공유된 자원의 데이터를 여러 스레드가 접근하는 것을 막는 방법
- Critical Section(각 프로세스에서 공유 데이터를 엑세스하는 프로그램 코드 부분)을 가진 쓰레드들의 Running time이 서로 겹치지 않게 각각 단독으로 실행되게 하는 기술

# 질문

### Race condition이란 무엇인가

두 개 이상의 스레드나 프로세스가 공유 자원을 사용할 때 발생하는 문제로, 실행 결과가 예측 불가능한 상태

### Race condition이 발생하는 이유

공유 자원에 대한 동시 접근이 일어나기 때문입니다. 동시에 여러 스레드나 프로세스가 공유 자원에 접근하면서 동시성 문제가 발생

[[운영체제] Race Condition과 예방할 방법(세마포어, 뮤텍스)](https://iredays.tistory.com/125)
