# 💡 시스템 콜(System Call)

# ✅ 시스템 콜(System Call)이란?
## 시스템 콜(System Call)
OS는 다양한 서비스들을 수행하기 위해 하드웨어를 직접적으로 관리한다. 이와 반면 응용 프로그램은 OS가 제공하는 인터페이스를 통해서만 자원을 사용할 수 있다.  
시스템 호출(System Call)은 운영체제의 커널이 제공하는 서비스에 대해, 응용 프로그램의 요청에 따라 커널에 접근하기 위한 인터페이스이다.

<br/>

시스템 콜은 커널 영역의 기능을 사용자 모드가 사용 가능하게 즉, 프로세스가 하드웨어에 직접 접근해서 필요한 기능을 할 수 있게 해 준다. (즉, 응용 프로그램은 시스템 콜을 사용해서 원하는 기능을 수행할 수 있다.)  
보통 직접적으로 시스템 콜을 사용하기보다는 API(라이브러리 함수)를 통해 사용하게 된다.

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bR6eVn/btrLzoAWyG7/kuPFQo2NrcnWpfrQideNzk/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bR6eVn/btrLzoAWyG7/kuPFQo2NrcnWpfrQideNzk/img.png)

위 그림처럼 운영체제(OS)는 메모리에 프로그램 적재, I/O처리, 파일 시스템 처리 등 여러 서비스들을 제공하는데 사용자 프로세스는 이에 직접적인 접근이 아닌 시스템 콜 호출을 통해 서비스를 제공받을 수 있다.

<br/>

사용자 프로그램이 디스크 파일을 접근하거나 화면에 결과를 출력하는 등의 작업이 필요한 경우, 즉, 사용자 프로그램이 특권 명령의 수행을 필요로 하는 경우, 운영체제에게 특권 명령의 대행을 요청하는 것이 시스템 콜이다.
- 통상적으로 시스템 콜은 여러 종류의 기능으로 나누어진다.
- 각 시스템 콜에는 번호가 할당되고 시스템 콜 인터페이스는 **시스템 콜 번호와 시스템 콜 핸들러 함수 주소로 구성되는 시스템 콜 테이블**을 유지한다.
- 운영체제는 자신의 커널 영역에서 해당 인덱스가 가리키는 주소에 저장되어 있는 루틴을 수행한다.
- 작업이 완료되면 CPU에게 인터럽트를 발생시켜 수행이 완료 되었음을 알린다.

<br/>

## 시스템 콜이 필요한 이유
우리가 일반적으로 사용하는 프로그램은 '응용프로그램'이다.  
유저 레벨의 프로그램은 유저 레벨의 함수들만으로는 많은 기능을 구현하기 힘들기 때문에 커널(Kernel)의 도움을 반드시 받아야 한다.   
이러한 작업은 응용 프로그램으로 대표되는 유저 프로세스(User Process)에서 유저 모드에서는 수행할 수 없다.  
반드시 Kernel에 관련된 것은 커널 모드로 전환한 후, 해당 작업을 수행할 권한이 생긴다.  
커널 모드를 통한 이러한 작업은 반드시 시스템 콜을 통해 수행하도록 설계되어 있다.

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/JXwNG/btqw787Kgfe/vmrkitiEEjDI8G9w2mFzUk/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/JXwNG/btqw787Kgfe/vmrkitiEEjDI8G9w2mFzUk/img.png)

<br/>

그렇다면 권한은 왜 필요한 것일까?  
그 이유는 해커가 피해를 입히기 위해 악의적으로 시스템 콜을 사용하는 경우나 초보 사용자가 하드웨어 명령어를 잘 몰라서 아무렇게 함수를 호출했을 경우, 시스템 전체를 망가뜨릴 수도 있기 때문이다. 따라서 이러한 명령어들은 특별하게 커널 모드에서만 실행할 수 있도록 설계되었고, 만약 유저 모드에서 시스템 콜을 호출할 경우에는 운영체제에서 불법적인 접근이라 여기고 Trap을 발생시킨다.

<br/>

## 시스템 콜의 목적
- 추상화된 하드웨어 인터페이스를 유저 프로세스에게 제공한다.
- 시스템의 보안과 안정성을 보장한다.
- 가상화된 유저 프로세스와 시스템이 소통할 수 있는 유일하고 공통적인 소통 수단

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bPksd5/btriq7nM7iL/3jPi9B86CI06ifUXerxSLK/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bPksd5/btriq7nM7iL/3jPi9B86CI06ifUXerxSLK/img.png)

<br/>

## 시스템 콜 종류
시스템 콜은 크게 6가지로 분류할 수 있다.

<br/>

### 프로세스 제어(Process Control)
- 프로세스 생성 및 종료
- 메모리에 로드, 실행
- 프로세스 속성 값 확인, 지정
- wait 이벤트, signal 이벤트
- 메모리 할당
- 예) fork, wait, exec 등

<br/>

### 파일 조작(File Manipulation)
- 파일 생성, 파일 삭제
- 열기, 닫기
- 읽기, 쓰기, Reposition
- 파일 속성 값 확인, 지정
- 예) open, read, write, close 등

<br/>

### 장치 관리(Device Manipulation)
- 디바이스 요청 및 해제
- 읽기, 쓰기, Reposition
- 디바이스 속성 확인, 지정
- 비물리적인 디바이스 해제 및 장착

<br/>

### 정보 유지(Information Maintenance)
- 시간 확인, 시간 지정
- 시스템 데이터 확인, 지정
- 프로세스, 파일, 디바이스 속성 가져오기
- 프로세스, 파일, 디바이스 속성 설정하기

<br/>

### 통신(Communication)
- 커뮤니케이션 연결 생성 및 삭제
- 메시지 송신, 수신
- 상태 정보 전달
- remote 디바이스 해제 및 장착

<br/>

### 보호(Protection)
- Permission 획득
- Permission 설정

<br/>

- UNIX System Call  
![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/cA9in9/btqw9OAIYdZ/kKNVkBl0y9k9R3EjTNyNI0/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/cA9in9/btqw9OAIYdZ/kKNVkBl0y9k9R3EjTNyNI0/img.png)

<br/>
<br/>

# ✅ 시스템 콜 동작
## open() 의 호출
![https://velog.velcdn.com/images/nnnyeong/post/31ad75d1-20d8-4029-803b-924aec68a5e6/image.png](https://velog.velcdn.com/images/nnnyeong/post/31ad75d1-20d8-4029-803b-924aec68a5e6/image.png)

<br/>

- 운영체제가 제공하는 시스템 콜에 대한 연결고리 역할을 하는 시스템 콜 인터페이스를 제공한다.
- 시스템 콜에는 번호가 할당되고 시스템 콜 인터페이스는 이 번호에 따라 색인되는 테이블을 유지한다.
- 시스템 콜 인터페이스는 의도하는 시스템 콜을 부르고 시스템 콜의 상태와 반환 값을 돌려준다.
- 사용자는 시스템 콜이 어떻게 구현되고 실행 중 무슨 작업을 하는지 알 필요가 없다.

<br/>

- open() 이라는 시스템 콜의 인덱스가 가리키는 곳에 이에 대한 처리 과정이 저장되어 있다.

<br/>

경우에 따라 시스템 콜이 발생했을 때, 추가적인 정보가 필요할 수도 있는데 그러한 정보가 담긴 매개변수들을 OS 에 어떻게 전달할까?
- 매개변수를 CPU 레지스터에 전달한다.
    - 전달해야 하는 매개변수 보다 레지스터의 수가 작을 수 있다.
- 매개변수를 메모리에 저장해 해당 메모리의 주소를 레지스터에 전달 할 수 있다.
- 매개변수는 프로그램에 의해 스택(stack)에 전달(push) 될 수도 있다.
    - 2, 3 번의 경우 매개변수의 개수나 길이의 제한이 없기 때문에 선호되는 방식이다.

<br/>

![https://velog.velcdn.com/images/nnnyeong/post/32ef9d02-5b36-4172-bcc7-613a7f9429f1/image.png](https://velog.velcdn.com/images/nnnyeong/post/32ef9d02-5b36-4172-bcc7-613a7f9429f1/image.png)

<br/>
<br/>

# 🗣 면접 예상 질문
## Q1. 인터럽트와 시스템 콜의 차이에 대해 설명해 주세요.
### Interrupt
Interrupt는 프로그램 실행 중에 CPU의 현재 처리 순서를 중단하고, 다른 동작을 수행하도록 요구하는 것이라고 볼 수 있다.  
즉, Interrupt가 발생하면 운영체제는 CPU에게 그동안 하고 있는 일들을 멈추고, Interrupt를 해결하도록 한다.

<br/>

### System Call
운영체제가 제공하는 서비스에 대한 프로그래밍 인터페이스가 System Call이고, System Call을 실행시키기 위한 CPU 명령어가 SVC이다.

<br/>

## Q2. 유닉스(Unix)에서 새로운 프로세스를 만드는 시스템 콜은 무엇인가요?
1. fork
2. create
3. new
4. generate

<br/>

[정답] 1  
[설명] 'fork'는 호출한 프로세스를 복제하여 새로운 프로세스를 만드는 시스템 콜이다. 호출한 프로세스는 부모 프로세스로 생성된 프로세스는 자식 프로세스로 언급된다. 스레드가 아니라 프로세스이기 때문에 분리된 메모리 영역을 가지고 실행된다.

<br/>

## Q3. 종료된 자식 프로세스(child process)의 정보를 얻어올 수 있는 시스템 콜(system call)은?
1. wait
2. exit
3. fork
4. get

<br/>

[정답] 1  
[설명] 'wait'은 자식 프로세스가 종료되기를 기다렸다가, 종료되면 자식 프로세스의 PID와 종료된 상태를 반환한다. 종료된 상태는 종료가 정상적이었는지, 비정상적이었는지 또는 시그널을 받아 종료되었는지 등의 다양한 정보를 포함한다.

<br/>
<br/>

# 🗂 참고
- [[Operating System] (iOS) System Call (시스템콜, 시스템 호출이란?) (tistory.com)](https://didu-story.tistory.com/311)
- [[OS] 시스템 콜, System Call (velog.io)](https://velog.io/@nnnyeong/OS-%EC%8B%9C%EC%8A%A4%ED%85%9C-%EC%BD%9C-System-Call)
- [3. 인터럽트 (Interrupt) :: JustZino (tistory.com)](https://justzino.tistory.com/4)
- [[운영체제] 시스템 콜 (System Call) (tistory.com)](https://fjvbn2003.tistory.com/306)
- [시스템 콜 (System Call) (tistory.com)](https://choiyeonho903.tistory.com/58)
- [오늘부터 전공면접 IT (hexoul.github.io)](https://hexoul.github.io/prepare-interview-data/os/1)
