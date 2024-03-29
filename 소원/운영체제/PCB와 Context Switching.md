# 💡 PCB와 Context Switching.md
# ✅ PCB

> 특정 프로세스에 대한 정보를 담고 있는 자료 구조
> 
- 운영체제가 프로세스를 제어하기 위해 정보를 저장해 놓는 곳으로, 프로세스의 상태 정보를 저장하는 구조체
- 프로세스 상태 관리와 문맥 교환을 위해 필요하다
- 프로세스 생성시 만들어지며 주기억 장치에 유지
- 프로세스가 생성될 때마다 고유의 PCB가 생성되어 메모리에 유지되고, 프로세스가 완료되면 제거된다

- 예를들어 CPU에 급한 프로세스 처리 때문에 긴급 요청이 들어왔을 때 기존에 작업하던 프로세스를 어딘가에 임시 저장해 놓아야 처리 후 다시 불러올 수 있다
- 즉, 프로세스에 관한 정보들을 저장할 공간이 필요
    
    → **PCB**
    
- PCB: 운영체제가 프로세스에 대한 중요한 정보를 저장해 놓을 수 있는 저장 장소를 뜻
- 한 PCB에는 한 프로세스의 정보가 담긴다
    
    ![25673A5058F211C224.png](https://t1.daumcdn.net/cfile/tistory/25673A5058F211C224)
    

## 진행 과정

1. 프로그램 실행
2. 프로세스 생성
3. 프로세스 주소 공간 (코드, 데이터, 스택) 생성
4. 이 프로세스의 메타데이터들이 PCB에 저장
    - 메타데이터: 데이터에 관한 구조화된 데이터

## 포함되는 정보

1. Process ID: 프로세스를 구분하는 ID
2. Process State: 각 State들의 상태 저장
3. Program Counter: 다음 Instruction의 주소를 저장하는 카운터. CPU는 이 값을 통해 Process의 Instruction을 수행
4. Register: Accumulator, CPU Register, General Register 등을 포함
    - CPU Register: CPU에서 사용한 레지스터의 값을 잃지 않기 위해 PCB에 그 값을 저장
5.  ****CPU Scheduling Information **:** 우선 순위, 최종 실행시간, CPU 점유시간 등이 포함
6. Memory Information: 해당 프로세스 주소 공간 정보를 저장
7. Process Information: 페이지 테이블, 스케줄링 큐 포인터, 소유자, 부모 등
8. Device I/O Status: 로세스에 할당된 입출력 장치 목록, 열린 팔린 목록 등
9. Pointer: 부모/자식 프로세스에 대한 포인터, 자원에 대한 포인터 등
10. Open File List: 프로세스를 위해 열려있는 파일의 리스트

## 필요한 이유

- CPU는 프로세스의 상태에 따라서 교체 작업이 이루어진다
- 이 때 교체되는 프로세스의 상태 값을 PCB에 저장해두었다가 앞으로 다시 수행할 때 사용

## 관리 방식

- Linked List 방식으로 관리
- 따라서 삽입, 삭제가 용이하며 프로세스가 생성되면 해당 PCB가 생성되고, 프로세스가 완료되면 제거된다

# ✅ Context Switching

> CPU를 차지하던 프로세스가 나가고 새로운 프로세스를 받아들이는 작업
> 
- 컴퓨터에서 여러 개의 프로세스를 처리해야 한다면, CPU는 프로세스를 시간 할당량에 따라 순차적으로 처리
- 이때 수많은 프로세스를 처리해야 한다면, 프로세스의 정보가 담긴 PCB가 있어야만 CPU는 PCB에서 얻은 정보를 바탕으로 프로세스를 처리할 수 있다
- 이때 작업 중인 프로세스를 중단하고 다른 프로세스를 실행할 때 문맥 교환이 일어난다
- 두 프로세스의 PCB를 교환하는 작업이 문맥 교환

## 문맥 교환의 절차

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdOJdBE%2Fbtrd5jd1QrK%2FKbu9vMTZ4TFXkqDlKkXuJk%2Fimg.png)

- 실행 상태에 있는 프로세스 P1이 자신에게 주어진 시간을 다 사용하여 타임 아웃이 된다면 P1의 PCB에 현재까지의 작업 결과가 저장되고 P1은 준비 상태로 쫓겨남
- 준비 상태에 있던 P2가 실행 상태로 가면 CPU의 레지스터가 P2의 프로세스 제어 블록으로 채워져 다음 작업을 하게 된다

## 발생하는 문제점

- 시간할당량: CPU를 차지하는 시간 간격
- 시간할당량에 따라 문맥 교환이 증가하거나 감소하면서 문제점이 발생한다
- 시간할당량이 작을수록 여러 개의 프로세스가 동시에 수행되는 느낌을 가질 수 있지만, 그에 따른 문맥 교환 수, 인터럽트 횟수, 오버헤드 증가
    - 오버헤드: 어떤 처리를 하기 위해 들어가는 간접적인 처리 시간, 메모리
    - 예를 들어 A라는 처리를 단순하게 실행핟나면 10초
    - 안정성을 고려하고 부가적인 B라는 처리를 추가한 결과 15초
    - 여기서 오버헤드는 5초
- 문맥 교환이 자주 일어나면, 다른 프로세스를 처리하기 위해 들어가는 시간 및 메모리가 증가하며, 이는 간접 부담을 증가 시키는 원인이 된다

- 하지만 프로세스 작업 중에는 오버헤드를 감수해야 하는 상황이 있음
    - 프로세스를 수행하다가 입출력 이벤트가 발생해서 대기 상태로 전환
    - 이때 CPU를 그냥 놀게 놔두는 것보다 다른 프로세스를 수행하는 것이 효율적
- 즉 계속 프로세스를 수행시키도록 다른 프로세스를 실행시키고 문맥 교환

# 질문

### 문맥 교환이란?

- CPU를 차지하던 프로세스가 나가고 새로운 프로세스를 받아들이는 작업

### 문맥 교환을 하는 이유?

- 프로세스가 사용되는 것처럼 하기 위해서는 CPU가 task를 바꿔가며 실행해야 함

**참고**

[운영체제  - PCB(Process Control Block)란?](https://dev-mystory.tistory.com/119)

[[운영체제] PCB와 Context Switching](https://velog.io/@klloo/운영체제-PCB와-Context-Switching)
