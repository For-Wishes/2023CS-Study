# 💡 IPC(Inter Process Communication)

# ✅ IPC란?
IPC는 Inter-Process Communication 의 줄임말로 프로세스 간의 통신을 위한 메커니즘을 의미한다. 즉, IPC는 프로세스 간의 통신을 돕는다. IPC는 다음과 같이 두 가지 모델이 존재한다.  
- Shared Memory
- Message Passing

<br/>

프로세스들은 independent(독립적)일 수도 있고 cooperating(상호 협조적)일 수도 있다.

  > 프로세스는 독립적으로 실행된다. 즉, 독립되어 있다는 것은 다른 프로세스에게 영향을 받지 않는다고 말할 수 있다. (스레드는 프로세스 안에서 자원을 공유하므로 영향을 받는다.)
  > 

cooperating한 프로세스들은 공유 data를 포함해 프로세스들끼리 영향을 준다.  
정보 공유, 속도 향상, 모듈화의 목적을 가지고 있다.  
이를 위해 Interprocess Communication(IPC)를 필요로 한다.

<br/>

![https://www.w3schools.in/wp-content/uploads/2017/10/communications-models.png?ezimgfmt=rs:520x330/rscb23/ng:webp/ngcb22](https://www.w3schools.in/wp-content/uploads/2017/10/communications-models.png?ezimgfmt=rs:520x330/rscb23/ng:webp/ngcb22)

<br/>

프로세스끼리 직접적으로 '대화'하는 방법은 없다. 왜 그렇냐면 프로세스들이 서로 공간을 쉽게 접근하면 프로세스의 데이터나 코드가 다른 프로세스에 의해 쉽게 바뀔 수 있기 때문이다.  
이를 막기 위해 프로세스는 통신을 직접적으로 할 수가 없고, 서로의 공간을 접근할 수가 없다. 그래도 프로세스 간의 커뮤니케이션은 필요하기 때문에 나온 기법이라 할 수 있다.

<br/>

### 프로세스 간 통신(커뮤니케이션)이 필요한 이유(IPC가 필요한 이유)
성능을 높이기 위해 존재한다. 어떤 로직을 하나의 프로세스로만 수행하는 대신, 여러 프로세스가 수행해서 보다 빠른 성능을 기대할 수 있다. 물론 이를 위해선 당연히 그 로직을 수행하는 과정에서 필요한 데이터들을 서로 공유할 수 있어야 한다. 그래서 이러한 기법이 필요한 거다.  
- 정보 공유(Information Sharing) :    
    여러 사용자가 동일한 정보에 액세스할 필요가 있을 수 있다.    
- 가속화(Computation Speed-up) :    
    특정 작업(task)을 여러 개의 서브 작업(sub-task)로 쪼개어 프로세스의 병렬성을 키움으로써 처리 속도를 높일 수 있다. 이때 메인 작업과 서브 작업은 서로 통신의 필요성이 생긴다.    
- 모듈화(Modularity) :    
    특정한 시스템 기능을 별도의 프로세스(스레드)로 구분하여 모듈화된 시스템을 구성할 수 있다. 이때 모듈 간의 통신이 필요하다.    
- 편의성(Convenience) :    
    다수의 사용자가 동시에 여러가지 작업을 수행할 수 있다.
    
<br/>    

## Shared Memory
ex : Semaphores 등  
Shared Memory 방식은 말 그대로 프로세스들이 공유하는 메모리를 이용해 통신하는 것이다. 이때 공유할 item을 생성하는 생산자(producer) 프로세스와 생성한 item을 소비하는 소비자(consumer) 프로세스가 나뉘게 된다. 즉, 생산자가 공유 메모리(buffer)에 item을 생산하고 저장하면, 소비자가 이를 읽고 소비하게 된다.

<br/>

이때 중요한 것은 동기화(synchronize)가 필요하다는 것이다.

<br/>

### 동기화 문제(Synchronization Problem)
동시에 공유 자원에 접근하는 것은 데이터의 일관성을 해칠 수 있다. 프로세스들의 실행 순서를 정하여 공유 자원의 일관성을 보장하는 것을 동기화(Synchronization)라고 한다.

<br/>

### 경쟁 상태(Race Condition)
여러 프로세스들이 공유 자원에 동시에 접근하려고 하는 상황을 경쟁 상태라고 한다. 어떤 프로세스가 마지막으로 데이터에 접근했는지에 따라 데이터의 상태가 달라지게 된다. 즉, 데이터의 일관성을 보장할 수 없어진다.  
이런 경쟁 상태의 문제를 해결하기 위해 프로세스들은 동기화(Synchronized)되어야 한다.

<br/>

### 임계 영역(Critical Section)
임계 영역은 공유 자원이 접근되는 부분을 뜻한다. 만약 어떤 프로세스가 임계 영역의 작업을 수행 중이라면 다른 프로세스는 해당 임계 영역에 들어와서는 안된다. 임계 영역을 구현하기 위해서는 3 가지 조건을 충족해야 한다.

<br/>

1. 상호 배제(Mutual Exclusion)    
    프로세스 P가 해당 임계 영역을 수행 중이라면, 다른 프로세스들은 해당 임계영역을 수행 해서는 안된다.
    
<br/>    

2. 진행(Progress)    
    어떠한 프로세스도 임계 영역을 수행하고 있지 않을 때, 임계 영역에 접근하고자 하는 프로세스가 있다면 해당 프로세스를 임계 영역에 들어갈 수 있게 해야 한다. 즉, 아무도 임계 영역에 없는데 프로세스가 임계 영역에 못 들어가면 안된다는 뜻이다.
    
<br/>

3. 한정 대기(Bounded Waiting)    
    한 프로세스만 계속 임계 영역을 수행하는 기아(Starvation) 문제를 방지하기 위해 한 번 임계 영역에 들어간 프로세스는 한정(bound)을 두어 다른 프로세스도 해당 임계 영역을 수행할 수 있도록 해야 한다.
    
<br/>

## Message Passing System
ex : Pipe, Signal, Message Queueing, Socket 등  
Message Passing 방식은 공유되는 주소 공간 없이 프로세스 간 통신할 수 있다. 이때 Message Passing 방식은 send(전송), receive(수신) 연산을 통해 통신하게 된다. 만약 프로세스 P와 Q가 통신하고 싶다면, 둘은 communication link를 둘 사이에 만들어야 한다.  
Message Passing System을 설계할 때 고려해야 할 3 가지는 다음과 같다.

<br/>

### Naming
- Direct Communication(직접 통신) : 프로세스 간 서로의 이름을 명확히(explicitly) 알고, 직접 통신한다.
    - send(P, Message) : 프로세스 P에게 메시지를 전송
    - receive(Q, Message) : 프로세스 Q로부터 메시지 수신
- Indirect Communication(간접 통신) : 메시지가 mailBox를 통해 송수신 된다.
    - 모든 mailBox 는 고유한 id를 가진다.
    - mailBox를 공유해야지만 프로세스 간에 통신할 수 있다.
    - send(A, Message) : mailBox A에게 메시지를 전송
    - receive(A, Message) : mailBox A로부터 메시지 수신

<br/>

### Synchronization
- Blocking : synchronous하다고 생각할 수 있다.
    - Blocking send : 메시지를 송신한 프로세스는 수신 측 프로세스가 메시지를 받을 때까지 기다린다.
    - Blocking receive : 수신 측 프로세스는 메시지를 받을 때까지 기다린다.
- Non-Blocking : asynchronous하다고 생각할 수 있다.
    - Non-Blocking send : 메시지를 송신한 프로세스는 다시 자기 할 일(operation)을 한다.
    - Non-Blocking receive : 수신 측 프로세스는 valid(유효한) 메시지나 NULL 메시지를 받는다.

<br/>

### Buffering
- Zero capacity : 0 개의 메시지
    - 송신 측은 무조건 수신자를 기다려야 한다.
- Bounded capacity : n 개의 메시지
    - 송신 측은 link 가 꽉차면 기다려야 한다.
- Unbounded capacity : 무한한 길이
    - 송신 측은 절대 기다리지 않는다.

<br/>

## IPC 모델 비교
| 공유 메모리(Shared Memory) | 메시지 전달(Message Passing) |
| --- | --- |
| 공유 메모리 영역을 구축하고 공유 영역을 통해 자원이나 데이터를 주고 받음 | 커널을 통해 메시지를 전달하는 방식으로 자원이나 데이터를 주고 받음 |
| 커널 의존도가 낮기 때문에 속도가 빠르고 통신이 자유로움 | 커널을 이용하기 때문에 구현이 비교적 쉬움 |
| 자원과 데이터를 공유하기 때문에 동기화 이슈 발생 | 시스템 콜이 필요하며 이로 인해 오버헤드 발생 |
| Semaphores 등 | Pipe, Signal, Message Queueing, Socket 등 |

<br/>
<br/>

# ✅ IPC 종류
프로세스는 커널이 제공하는 IPC 설비를 이용해 프로세스간 통신을 할 수 있게 된다.

> 커널이란?
운영체제의 핵심적인 부분으로, 다른 모든 부분에 여러 기본적인 서비스를 제공해 준다.
> 

<br/>

IPC 설비 종류도 여러 가지가 있다. 필요에 따라 IPC 설비를 선택해서 사용해야 한다.

<br/>

## PIPE
파이프는 두 개의 프로세스를 연결하는데 하나의 프로세스는 데이터를 쓰기만 하고, 다른 하나는 데이터를 읽기만 할 수 있다.  
한쪽 방향으로만 통신이 가능한 반이중 통신이라고도 부른다.  
따라서 양쪽으로 모두 송/수신을 하고 싶으면 2개의 파이프를 만들어야 한다.  
매우 간단하게 사용할 수 있는 장점이 있고, 단순한 데이터 흐름을 가질 땐 파이프를 사용하는 것이 효율적이다. 단점으로는 전이중 통신을 위해 2개를 만들어야 할 때는 구현이 복잡해지게 된다.

<br/>

## Named PIPE
익명 파이프는 통신할 프로세스를 명확히 알 수 있는 경우에 사용한다. (부모-자식 프로세스 간 통신처럼)  
Named 파이프는 전혀 모르는 상태의 프로세스들 사이 통신에 사용한다.  
즉, 익명 파이프의 확장된 상태로 부모 프로세스와 무관한 다른 프로세스도 통신이 가능한 것이다. (통신을 위해 이름 있는 파일을 사용)  
하지만, Named 파이프 역시 읽기/쓰기 동시에 불가능함. 따라서 전이중 통신을 위해서는 익명 파이프처럼 2개를 만들어야 가능하다.

<br/>

## 시그널
프로세스 ID를 통해 특정 프로세스에 메시지를 전달하는 방식

<br/>

## Message Queue
입출력 방식은 Named 파이프와 동일함  
다른 점은 메시지 큐는 파이프처럼 데이터의 흐름이 아니라 메모리 공간이다.  
사용할 데이터에 번호를 붙이면서 여러 프로세스가 동시에 데이터를 쉽게 다룰 수 있다.

<br/>

## Shared Memory(공유 메모리)
파이프, 메시지 큐가 통신을 이용한 설비라면, 공유 메모리는 데이터 자체를 공유하도록 지원하는 설비다.  
프로세스의 메모리 영역은 독립적으로 가지며 다른 프로세스가 접근하지 못하도록 반드시 보호되어야 한다. 하지만 다른 프로세스가 데이터를 사용하도록 해야 하는 상황도 필요할 것이다. 파이프를 이용해 통신을 통해 데이터 전달도 가능하지만, 스레드처럼 메모리를 공유하도록 해준다면 더욱 편할 것이다.  
공유 메모리는 프로세스 간 메모리 영역을 공유해서 사용할 수 있도록 허용해준다.  
프로세스가 공유 메모리 할당을 커널에 요청하면, 커널은 해당 프로세스에 메모리 공간을 할당해 주고 이후 모든 프로세스는 해당 메모리 영역에 접근할 수 있게 된다.  
중개자 없이 곧바로 메모리에 접근할 수 있어서 IPC 중에 가장 빠르게 작동한다.

<br/>

## Memory Map
공유 메모리처럼 메모리를 공유해준다. 메모리 맵은 열린 파일을 메모리에 맵핑시켜서 공유하는 방식이다. (즉 공유 매개체가 파일+메모리)  
주로 파일로 대용량 데이터를 공유해야 할 때 사용한다.

<br/>

## Socket
네트워크 소켓 통신을 통해 데이터를 공유한다.  
클라이언트와 서버가 소켓을 통해서 통신하는 구조로, 원격에서 프로세스 간 데이터를 공유할 때 사용한다.  
서버(bind, listen, accept), 클라이언트(connect)

<br/>

> 이러한 IPC 통신에서 프로세스 간 데이터를 동기화하고 보호하기 위해 세마포어와 뮤텍스를 사용한다. (공유된 자원에 한번에 하나의 프로세스만 접근시킬 때)
> 

<br/>
<br/>

# 🗣 면접 예상 질문
## Q1. IPC란 무엇이고, 예시는 무엇이 있나요?
IPC는 프로세스들 사이에 서로 데이터를 주고 받는 방식 즉, 프로세스 간의 통신을 의미한다. 각 프로세스는 독립적인 실행 객체이기 때문에 프로세스 간 통신을 하려면 커널이 제공하는 IPC 모델 방식을 사용해서 통신을 해야 한다.  
IPC는 크게 두 가지 모델로 나눌 수 있다. 첫째는 주소 공간의 일부를 공유하며 공유한 메모리 영역에 읽기/쓰기를 통해 통신하는 공유 메모리 모델이 있다. 공유 메모리 모델의 예시로는 공유 메모리와 POSIX가 있다. 두 번째로는 메시지 전송 모델이다. 커널 메모리 영역에 메시지 전달을 위한 채널을 만들어서 송수신자 간에 전송/수신을 통해 통신하는 방식이다. 예시로는 파이프, 메시지 큐, 소켓 등이 있다.

<br/>
<br/>

## Q2. IPC 두 모델의 장단점을 설명해 주세요.
- 공유 메모리 모델의 경우, 커널의 관여 없이 메모리를 직접 사용하여 통신하기 때문에 통신 속도가 빠른 장점이 있지만, 별도의 동기화 과정이 필요하며 동시에 메모리 위치를 접근하는 문제가 발생할 수 있다는 단점이 있다. 따라서 별도의 접근 제어 방법이 필요하며, 접근 제어 방식은 locking이나 세마포어(semaphore) 등이 있다.
- 메시지 전달 모델의 경우, 커널을 통해서 데이터를 주고 받기 때문에 통신 속도가 느리다는 단점이 있지만, 커널에서 데이터를 주고 받는 과정을 컨트롤할 수 있어 안전하며 send/receive 연산에 대해 커널이 동기화를 제공해 준다는 장점이 있다.

<br/>
<br/>

# 🗂 참고
- [[운영체제] IPC(Inter-Process Communication)란? | pipes (tistory.com)](https://code-lab1.tistory.com/42)
- [Interprocess communication (IPC) (w3schools.in)](https://www.w3schools.in/operating-system/interprocess-communication-ipc)
- [[운영체제] 동기화 문제(Synchronization problem), 경쟁 상태(Race Condition), 임계 영역(Critical Section) (tistory.com)](https://code-lab1.tistory.com/50)
- [[운영체제] IPC 기법 (velog.io)](https://velog.io/@redgem92/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-IPC-%EA%B8%B0%EB%B2%95)
- [IPC(Inter Process Communication) | 👨🏻‍💻 Tech Interview (gyoogle.dev)](https://gyoogle.dev/blog/computer-science/operating-system/IPC.html)
- [IPC(Inter-Process Communication)란? (tistory.com)](https://y-oni.tistory.com/77)
- [[프로세스간 통신] IPC(inter process communication) 종류 (tistory.com)](https://doitnow-man.tistory.com/110)
- [[운영체제] IPC (tistory.com)](https://steady-coding.tistory.com/508)
