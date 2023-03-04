# 💡 PCB와 Context Switching

# ✅ PCB(Process Control Block)
## 프로세스 관리
구동 중인 프로세스가 여러 개일 때, CPU 스케줄링을 통해 프로세스를 관리하는 것을 의미한다. 당연하게도 CPU 들은 각 프로세스들에 대해서 구분할 수 있어야 지지고 볶고 관리가 가능하다. 따라서 각기 다른 프로세스들의 본연의 특징을 갖고 있는 `Process Metadata`라는 정보를 활용한다.

<br/>

메타 데이터는 프로세스가 생성될 때마다 PCB(Process Control Block)라는 곳에 저장된다.

<br/>

## PCB(Process Control Block)
PCB(Process Control Block) 혹은 TCB(Task Control Block)는 특정 프로세스에 대한 정보를 담고 있는 자료구조이다. 운영체제는 PCB에 담긴 프로세스 정보를 이용하여 프로세스를 관리/제어한다. 프로세스가 생성될 때마다 고유의 PCB가 생성되고 프로세스가 완료되면 제거된다. PCB는 프로세스의 중요한 정보를 포함하고 있으므로 일반 사용자가 접근하지 못하는 보호된 메모리 영역에 존재한다.

<br/>

### Process Metadata가 담고 있는 정보
- Process id - 프로세스 고유 ID(PID)
- Process state - 프로세스의 상태(new ready waiting, running, terminated)
- Program Counter(PC) - 다음 명령의 주소를 가리키고 있는 계수기
- CPU register - CPU 레지스터
- CPU-scheduling - 프로세스의 우선순위, 최종 실행 시간, 스케줄링 큐를 가리키는 포인터 등
- Memory-management - register, 페이지 테이블, 세그먼트 테이블의 base, limit 값에 대한 정보
- Accounting - CPU 사용 시간, 실제 사용된 시간, 시간 제한 등
- I/O status - 프로세스에 할당된 I/O 기기에 해당하는 정보

<br/>

![https://velog.velcdn.com/images/heetaeheo/post/5e655d92-2e92-4bdc-bc37-07031dc8d9a4/image.png](https://velog.velcdn.com/images/heetaeheo/post/5e655d92-2e92-4bdc-bc37-07031dc8d9a4/image.png)

<br/>

PCB는 프로세스들의 메타 데이터를 저장하는 곳이며, 한 PCB 안에는 한 프로세스의 정보가 담기게 되는 구조이다. 프로그램이 실행되어 메모리에 적재됐을 때 프로세스가 생겨나고, 프로세스 주소 공간에 코드 & 데이터 & 스택 공간이 생성된다. 이후 해당 프로세스의 메타 데이터들이 PCB에 저장된다.

<br/>

![https://velog.velcdn.com/images/haero_kim/post/dd3d9ba6-bb62-4ade-bce7-341a2e1a3751/25673A5058F211C224.png](https://velog.velcdn.com/images/haero_kim/post/dd3d9ba6-bb62-4ade-bce7-341a2e1a3751/25673A5058F211C224.png)

<br/>

CPU 에서는 프로세스의 상태에 따라 프로세스 교체 작업이 이루어지게 된다. 만약 어떤 프로세스로부터 인터럽트가 발생해서 현재 프로세스가 잠시 대기 상태가 되고 인터럽트가 발생된 프로세스를 실행 상태로 바꿔치기 할 때, 대기 중인 프로세스의 정보를 잃어버리게 되면 프로그램을 처음부터 다시 시작해야 한다. 이렇게 되면 사용자 입장에선 당혹스러울 것이다.  
따라서 대기하다가 다시 실행할 때 대기 상태로 바뀌기 직전의 실행 정보를 고스란히 저장해 둔다면 다시 실행 상태로 돌아왔을 때 아무 일도 없었단 듯이 흘러갈 수 있을 것이다. 이 동작을 위해 PCB가 필요한 것이다.

<br/>

## PCB의 관리 방식
한 프로세스에 한 PCB가 생성된다. 따라서 PCB는 프로세스가 생성될 때마다 하나씩 늘어나게 되는데, 이때 PCB 들을 관리하는 자료구조는 바로 Linked List 형태이다. PCB List Head에 PCB들이 생성될 때마다 하나씩 이어서 붙게 된다. 주소 값으로 연결되는 형태이기 때문에 새로운 녀석이 들어오거나 기존의 녀석이 나갈 때 뛰어난 효율을 보이게 된다. (삽입 삭제에 용이한 Linked List의 특성 활용)

<br/>

당연한 이야기지만, 프로세스가 종료된다면 PCB 도 제거된다.

<br/>

## PCB의 필요성
프로세스가 여러 개 생성될 때, 즉, 여러 개의 프로그램이 실행되고 있을 때, CPU는 프로세스의 상태에 따라 교체 작업을 수행한다.  
> 교체 작업 : Interrupt 발생 → 할당 받은 프로세스 Waiting 상태로 변경 → 다른 프로세스를 Running 상태로 변경
> 

<br/>

따라서 수행 대기 중인 프로세스에 관한 저장 값을 PCB에 저장해 두어야 한다.

<br/>

PCB는 LinkedList 방식으로 관리되어 삽입과 삭제가 용이하다. 따라서 프로세스가 생성될 때 PCB List Head에 PCB가 삽입되고 프로세스가 완료되면 PCB가 삭제되는 식으로 관리된다.

<br/>
<br/>

# ✅ Context Switching
> 문맥(Context)  
: 현재 CPU가 실행하고 있는 프로세스의 정보
> 

<br/>

현재 CPU가 현재 실행하고 있는 프로세스의 정보를 문맥이라고 하니 이를 교환하는 행위를 문맥 교환이라고 정의 내릴 수 있겠다. 현재 실행 중인 프로세스의 정보를 담고 있는 CPU 레지스터의 내용이 다음 실행할 프로세스의 정보로 변경되는 것을 의미한다.

<br/>

예를 들어 `프로세스 A`를 실행 중이던 CPU가 `프로세스 B`를 실행하기 위해 `프로세스 A`의 정보를 `어딘가`에 저장하고, `프로세스 B`의 정보를 `어딘가`로부터 꺼내온다. 여기서 말하는 `어딘가`가 바로 PCB이다.

<br/>

다양한 사람들이 동시에 사용하는 것처럼 하기 위해서 Context Switching이 필요하게 되었다.  
- 컴퓨터 멀티태스킹을 통해 빠른 반응 속도로 응답 가능하다.
- 빠르게 Task를 바꾸면서 실행하기에 사람은 실시간 처리가 되는 것처럼 보인다.
- CPU가 Task를 바꿔가며 실행하기 위해 Context Switching이 필요하게 되었다.

<br/>

## Context Switching이 필요한 이유
CPU는 한 번에 하나의 프로세스만 수행할 수 있지만 실생활에서 우리는 여러 개의 프로세스를 동시에 수행하는 것처럼 보이게 하기 위해서 Context Switching을 사용한다.

<br/>

## Context Switching은 언제 발생하는가?
실행되고 있는 프로세스가 빠지고 새로운 프로세스가 CPU를 받을 때 발생한다. CPU 스케줄링에 의해 할당된 작업 시간에 끝나 TimeOut이 발생하거나, 프로세스의 작업이 끝났거나, 실행 중이던 프로세스가 입출력 요청을 하는 등의 이유로 interrupt가 발생했을 때 Context Switching이 이루어진다.  
보통 인터럽트 발생 혹은 현재 프로세스의 선점 허용 기간을 모두 소모한 상황, 입출력을 위해 대기하는 경우에 Context Switching이 발생하게 된다.

<br/>

## 문맥 교환 절차
1. P0 프로세스가 인터럽트되면서 PCB0에 P0 프로세스의 상태 정보를 저장한다.
2. 다음 수행할 P1 프로세스의 PCB1에서 P1 프로세스의 상태 정보가 CPU에 재로딩된다.
3. P1 프로세스를 일정 시간 수행한다.
4. P1 프로세스가 인터럽트되면서 PCB1에 P1 프로세스의 상태 정보를 저장한다.
5. 다음 수행할 P0 프로세스의 PCB0에서 P0 프로세스의 상태 정보가 CPU에 재로딩된다.
6. P0 프로세스를 일정 시간 수행한다.

<br/>

![https://junhyunny.github.io/images/process-control-block-and-context-switching-2.JPG](https://junhyunny.github.io/images/process-control-block-and-context-switching-2.JPG)

<br/>

## Context Switching 문제점
Context Switching을 하는 동안에는 CPU 가 아무것도 하지 못하게 된다. 따라서 만일 스레드 및 프로세스의 개수가 엄청 많아져 Context Switching이 빈번히 일어나게 된다면, 오버헤드가 잦아져 성능이 악화될 가능성도 있다. 이를 Context Switching Overhead라고 한다.

<br/>

### Context Swiching과 시간 할당량
프로세스들의 시간 할당량은 시스템 성능의 중요한 역할을 한다. 시간 할당량이 적을 수록 사용자 입장에서는 여러 개는 프로세스가 거의 동시에 수행되는 느낌을 갖지만 인터럽트의 수와 문맥 교환의 수가 늘어난다. 프로세스의 실행을 위한 부가적인 활동을 오버헤드(간접 부담 비용)이라고 하는데, 이 또한 문맥 교환 수와 같이 늘어나게 된다.  
- 시간 할당량이 적어지면    
    : 문맥 교환 수, 인터럽트 횟수, 오버헤드가 증가하지만 여러 개의 프로세스가 동시에 수행되는 느낌을 갖는다.    
- 시간 할당량이 커지면    
    : 문맥 교환 수, 인터럽트 횟수, 오버헤드가 감소하지만 여러 개의 프로세스가 동시에 수행되는 느낌을 갖지 못한다.
    
<br/>
<br/>

# 🗣 면접 예상 질문
## Q1. PCB(Process Control Block)란 무엇이고, 왜 필요한가요?
PCB는 운영체제가 프로세스를 제어하기 위해 이전 작업에 대한 정보를 저장해 놓은 곳으로, 프로세스 메타 데이터(상태 정보)들을 저장하는 구조체다. 이것은 프로세스 상태 관리와 문맥 교환(Context Switching)을 위해 필요하다.  
PCB에 저장되는 정보는 PID(프로세스 고유 번호), 상태(준비, 대기, 실행, …), 포인터, 우선 순위, 레지스터 관련 정보 등이 있다.

<br/>

Context Switching이란 CPU가 이전의 프로세스 상태를 PCB에 보관하고, 또 다른 프로세스의 정보를 PCB에서 읽어 레지스터에 적재하는 과정을 말한다.  
인터럽트 발생, 실행 중인 CPU 사용 허가 시간 모두 소모, 입출력을 위해 대기하는 경우 등을 예로 들 수 있다.

<br/>

## Q2. Process Context Swtiching과 Thread Context Switching을 비교해서 말씀해 주세요.
Process가 Context Switching에 쓰이는 비용이 Thread보다 많이 든다. Thread는 Stack 영역을 제외한 모든 메모리를 공유하기에 Context Switching 발생 시 Stack 부분만 동작하면 되기 때문이다.

<br/>
<br/>

# 🗂 참고
- [PCB(Process Control Block) and Context Switching - Junhyunny’s Devlogs](https://junhyunny.github.io/information/operating-system/process-control-block-and-context-switching/)
- [PCB 와 Context Switching 알아보기 (velog.io)](https://velog.io/@haero_kim/PCB-%EC%99%80-Context-Switching-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0)
- [PCB 와 Context Switching (velog.io)](https://velog.io/@heetaeheo/PCB-%EC%99%80-Context-Switching)
- [JE의 끄적끄적 (tistory.com)](https://jungeun960.tistory.com/109)
