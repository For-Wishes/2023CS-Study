# 💡 CPU 스케줄링

# ✅ CPU 스케줄링이란?
CPU 이용률을 극대화하기 위해서는 멀티 프로그래밍(multiprogramming)이 필요하다.  
하지만 만약 CPU core가 하나라면 한 번에 하나의 프로세스만 실행 가능할 것이다. 이때 필요한 것이 CPU 스케줄링이다.  
즉, CPU 스케줄링은 언제 어떤 프로세스에 CPU를 할당할지 결정하는 작업이라고 할 수 있다.

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/A7pt2/btrlyZNmWBZ/zm11oSJnSpKYbLWWzzPsO1/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/A7pt2/btrlyZNmWBZ/zm11oSJnSpKYbLWWzzPsO1/img.png)

CPU 스케줄링 대상 프로세스는 Ready Queue에 있는 프로세스들로, 스케줄링 정책에 따라 Queue에 정렬을 한 후 앞에 있는 프로세스부터 CPU를 주게 된다.

<br/>

CPU 이용률을 최대화 하는 것은 다중 프로세서 운영체제 설계의 핵심이 된다. 

<br/>

## Dispatcher
스케줄러에는 멀티 프로그래밍에 이용되는 long-term 스케줄러와 CPU 스케줄링에 이용되는 short-term 스케줄러가 있다.

<br/>

> 넓은 의미의 스케줄링 = 스케줄링(Ready Queue 정렬) + Dispatch(프로세스를 CPU에 올림)
> 

<br/>

## CPU - I/O 버스트 사이클(CPU - I/O Burst Cycle)
프로세스 실행은 CPU 실행과 I/O 대기의 사이클로 구성된다.  
프로세스의 실행은 CPU Burst로 시작된다. 뒤이어 I/O Burst가 발생하고, 그 뒤를 이어 또 다른 CPU Burst가 발생하며, 이어 또 다른 I/O Burst 등등으로 진행된다. 결국 아래의 그림처럼 마지막 CPU Burst는 실행을 종료하기 위한 시스템 요청과 함께 끝난다.

![https://imbf.github.io/assets/computer-science/CPU-Scheduling-1.png](https://imbf.github.io/assets/computer-science/CPU-Scheduling-1.png)

<br/>

CPU Burst들의 지속시간을 광범위하게 측정한 그래프는 CPU 스케줄링 알고리즘을 구현할 때 매우 중요하다.

<br/>

## CPU 스케줄링 목적
CPU 스케줄러는 프로세스가 생성된 후 종료될 때까지 모든 상태 변화를 조정하는 일을 한다. 이 스케줄러가 하는 CPU 스케줄링은 어떤 프로세스에 CPU를 배정할지 결정하고, 이 작업은 컴퓨터 시스템의 효율에 직결되는 중요한 일이다.  
CPU 스케줄링의 본 목적은 모든 프로세스가 공평하게 작업할 수 있도록 하는 것이다. 하지만 안정성과 효율성을 높이기 위해 공평성의 일부분을 희생해야 한다. 다음은 스케줄링이 추구하는 목적들이다.

<br/>

- 공평성    
    : 모든 프로세스가 자원을 공평하게 배정받아야 하며 특정 프로세스가 배제되어서는 안 된다.    
- 효율성    
    : 시스템 자원을 놀리는 시간 없이 스케줄링해야 한다.    
- 안정성    
    : 우선 순위를 사용하여 중요한 프로세스가 먼저 처리되도록 해야 한다.    
- 반응 시간 보장    
    : 응답이 없는 경우 사용자는 시스템이 멈춘 것으로 가정하기 때문에 시스템은 적절한 시간 안에 프로세스의 요구에 반응해야 한다.    
- 무한 연기 방지    
    : 특정 프로세스의 작업이 무한히 연기되어서는 안 된다.
    
<br/>

## CPU 스케줄링 단계
### 고수준 스케줄링(long-term scheduling, job scheduling, admissin scheduling, high level scheduling)
가장 큰 틀에서 이루어지는 CPU 스케줄링으로 시스템 내의 전체 작업 수를 조절한다. 시스템 과부하를 막기 위해 어떤 작업을 시스템이 받아들일지 또는 거부할지를 결정하므로 시스템 내에서 동작 시에 실행 가능한 프로세스의 총 개수가 정해진다.

<br/>

### 중간 수준 스케줄링(middle level scheduling)
중지(suspend)와 활성화(active)로 전체 시스템의 활성화된 프로세스 수를 조절한다. 이로 인해 저수준 스케줄링이 원만하게 이루어지도록 완충하는(buffer) 역할을 한다.

<br/>

### 저수준 스케줄링(short-term scheduling, low level scheduling)
가장 작은 단위의 스케줄링으로 어떤 프로세스에 CPU를 할당할지, 어떤 프로세스를 대기 상태로 보낼지 등을 결정하는 역할이다. 중간 수준의 스케줄링은 프로세스를 보류 상태로 보내고, 저수준 스케줄링은 대기 상태로 보낸다. 스케줄링에 대해 공부하는 대부분의 내용이 이 저수준 스케줄링에 해당한다.

<br/>

## 스케줄링 시 고려 사항
### preemptive vs non-preemptive
- 선점형 스케줄링    
    : 프로세스가 CPU를 할당받아 실행 중이더라도 운영체제가 CPU를 강제로 빼앗을 수 있는 방식    
    CPU 처리 시간이 매우 긴 프로세스가 CPU 사용 독점을 막을 수 있어 효율적인 운영이 가능하다.    
    하지만 잦은 문맥 교환으로 오버헤드가 많이 발생한다.    
- 비선점형 스케줄링    
    : 프로세스가 CPU를 점유하고 있다면 이를 빼앗을 수 없는 방식    
    필요한 문맥 교환만 일어나기 때문에 오버헤드가 상대적으로 적지만 프로세스의 배치에 따라 효율성 차이가 많이 난다.    

<br/>

### CPU bound vs I/O bound
프로세스가 대기 상태에 있다가 CPU를 할당받아 실행하면 CPU burst, 입출력 작업을 하면 I/O burst라고 한다.

<br/>

- CPU bound process(CPU 집중 프로세스)    
    : CPU를 많이 사용하여 CPU burst가 많은 프로세스    
- I/O bound process(입출력 집중 프로세스)    
    : 입출력을 많이 사용해 I/O burst가 많은 프로세스
    
<br/>

두 프로세스가 같이 대기 상태에 있다면 입출력 집중 프로세스에 먼저 CPU를 할당시키는 것이 더 효율적이다. 왜냐하면 입출력 집중 프로세스는 CPU를 빠르게 쓰고 입출력 버스트를 하러 나가기 때문에 다른 프로세스가 오래 기다리지 않아도 된다.

<br/>

### 전면 프로세스 vs 후면 프로세스
- 전면 프로세스    
    : GUI를 사용하는 운영체제에서 화면의 맨 앞에 놓여 현재 입출력이 사용되고, 사용자와 상호작용이 가능해 상호작용 프로세스라고도 불림 (워드 프로세스)    
- 후면 프로세스    
    : 사용자의 입력 없이 작동하여 일괄 작업 프로세스라고 불림 (압축 프로세스)
    
<br/>

전면 프로세스는 사용자의 요구에 즉각 즉각 반응해야 하지만 후면 프로세스는 그럴 필요가 없다. 따라서 전면 프로세스를 먼저 처리해 줘야 한다.

<br/>

### 프로세스 우선 순위
CPU 스케줄러 대부분은 프로세스에 우선 순위를 매겨 우선 순위가 높은(우선 순위 숫자가 작은) 프로세스부터 처리되도록 한다.  
커널 프로세스 > 일반 프로세스  
전면 프로세스 > 후면 프로세스  
대화형 프로세스 > 일괄 처리 프로세스  
입출력 집중 프로세스 > CPU 집중 프로세스

<br/>

## CPU 스케줄러

![https://velog.velcdn.com/images/yu-jin-song/post/796496fc-0f74-4977-b9e9-b7be8dc02a16/프로세스_상태전이도.png](https://velog.velcdn.com/images/yu-jin-song/post/796496fc-0f74-4977-b9e9-b7be8dc02a16/프로세스_상태전이도.png)

<br/>

CPU 스케줄러는 메모리에 있는 프로세스들 중 어떤 프로세스를 실행할지 선택하고 CPU를 할당해 주는 역할을 한다.  
CPU 스케줄러는 프로세스들이 다음과 같은 상황에 있을 때 스케줄링을 결정한다.  
1. 실행(running) 상태에서 대기(waiting) 상태로 전환(switching)될 때 ( ex : I/O 발생 )
2. 실행(running) 상태에서 준비(ready) 상태로 전환(switching)될 때 ( ex : intterupt 발생 )
3. 대기(waiting) 상태에서 준비(ready) 상태로 전환(switching)될 때 ( ex : I/O 완료 시 )
4. 종료(Terminated)될 때

<br/>

1번과 4번 상황에서만 스케줄링이 발생하는 것을 비선점형(non-preemptive) 스케줄링이라고 한다.  
이외의 모든 스케줄링은 선점형(preemptive) 스케줄링이라고 한다.

<br/>

### 비선점형 스케줄링
프로세스가 CPU를 점유하고 있다면 이를 빼앗을 수 없는 방식  
필요한 문맥 교환만 일어나므로 오버헤드(overhead)가 상대적으로 적지만 프로세스의 배치에 따라 효율성 차이가 많이 난다.

<br/>

### 선점형 스케줄링
프로세스가 CPU를 할당받아 실행 중이더라도 운영체제가 이를 강제로 빼앗을 수 있는 방식  
CPU 처리 시간이 매우 긴 프로세스의 CPU 사용 독점을 막을 수 있어 효율적인 운영 가능  
잦은 문맥 교환으로 오버헤드(Overhead)가 커질 수 있다.

<br/>
<br/>

# ✅ CPU 스케줄링 알고리즘
## CPU 스케줄링 평가 기준(CPU Scheduling Criteria)
### CPU의 입장
1. CPU 이용률(CPU utilization)
    - 시간당 CPU를 사용한 시간의 비율
    - 프로세서를 실행 상태로 항상 유지하려고 해야 한다.
2. 처리율(Throughput)
    - 시간당 처리한 작업의 비율
    - 단위 시간당 완료되는 작업 수가 많도록 해야 한다.

### 프로세스의 입장
3. 반환 시간(Turnaround Time)
    - 프로세스가 생성된 후 종료되어 사용하던 자원을 모두 반환하는 데까지 걸리는 시간
    - 작업이 준비 큐(ready queue)에서 기다린 시간부터 CPU에서 실행된 시간, I/O 작업 시간의 합이다.
4. 대기 시간(Waiting Time)
    - 대기열에 들어와 CPU를 할당받기 까지 기다린 시간
    - 준비 큐에서 기다린 시간의 총합
5. 반응 시간(Response Time)
    - 대기열에서 처음으로 CPU를 얻을 때까지 걸린 시간
    - 대기 시간과 비슷하지만 다른 점은, 대기 시간은 준비 큐에서 기다린 모든 시간을 합친 것이지만 반응 시간은 CPU를 할당받은 최초의 순간까지 기다린 시간 한번 만을 측정한다.

<br/>

CPU 이용률과 처리율은 극대화하는 것이 좋고 반환 시간, 대기 시간, 반응 시간은 줄이는 것이 일반적으로 좋다.

<br/>

CPU 알고리즘의 효율성을 평가할 때 사용률과 처리량은 계산하기 어렵기 때문에 주로 대기 시간, 응답 시간, 반환 시간을 계산한다.  
- 대기 시간    
    : 프로세스가 생성된 후 실행되기 전까지 대기하는 시간    
- 응답 시간    
    : 첫 작업을 시작한 후 첫 번째 출력(반응)이 나오기까지의 시간    
- 실행 시간    
    : 프로세스 작업이 시작된 후 종료되기까지의 시간    
- 반환 시간    
    : 대기 시간을 포함하여 실행이 종료될 때까지의 시간
    
<br/>

## 스케줄링 알고리즘
### 스케줄링 알고리즘 종류
| 구분 | 종류 |
| --- | --- |
| 비선점형 알고리즘 | FCFS 스케줄링, SJF 스케줄링, HRN 스케줄링 |
| 선점형 알고리즘 | 라운드 로빈 스케줄링, SRT 스케줄링, 다단계 큐 스케줄링, 다단계 피드백 큐 스케줄링 |
| 둘 다 가능 | 우선 순위 스케줄링 |

<br/>

### FCFS(First Come First Served) 스케줄링
말 그대로 선입선출 방식으로, 준비 큐에 도착한 순서대로 CPU를 할당하는 비선점형 방식이다. 선입선출 스케줄링이라고도 한다. 모든 프로세스의 우선 순위가 동일하고, 프로세스의 CPU 처리 시간을 따로 고려하지 않기 때문에 매우 단순하고 공평한 방법이다.  
하지만 CPU 처리 시간이 긴 프로세스가 앞에 올 경우 뒤의 프로세스가 한없이 기다려야 하기 때문에 비효율적이게 된다. 이를 **콘보이 효과**라고 한다.

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/dufF6d/btqtWhgy7Zl/BMv2BKEl9fSAF3GxFKIwjk/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/dufF6d/btqtWhgy7Zl/BMv2BKEl9fSAF3GxFKIwjk/img.png)

<br/>

그림에서 보이듯이 CPU 버스트 타임이 2ms인 P4는 잠깐만 CPU를 얻으면 빠르게 처리하고 나갈 수 있지만 4 번째로 도착했기 때문에 30ms나 대기해야 한다.

<br/>

### SJF(Shortest Job First) 스케줄링
준비 큐에 있는 프로세스 중 실행 시간이 가장 짧은 작업부터 CPU를 할당하는 비선점형 방식이다. 늦게 도착하더라도 CPU 처리 시간이 앞에 대기 중인 프로세스보다 짧으면 먼저 CPU를 할당받을 수 있다. 때문에 콘보이 효과를 완화할 수 있다.  
단, 비선점형 방식이기 때문에 CPU를 사용 중인 프로세스보다 처리 시간이 짧더라도 빼앗지는 못한다.

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bzYkhC/btqtY8oiA3Q/4kZqk2gBuwj0klLXZzVUN0/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bzYkhC/btqtY8oiA3Q/4kZqk2gBuwj0klLXZzVUN0/img.png)

<br/>

위의 그림은 만약 모든 프로세스가 0초에 동시 도착했다는 가정이다. 그럴 경우 P4가 버스트 타임이 가장 짧기 때문에 먼저 실행되고, P1이 가장 나중에 실행된다. 평균 대기 시간을 위의 FCFS와 비교해보면 월등히 짧은 것을 알 수 있다.  
하지만 만약 P1이 가장 먼저 도착했다면 어쩔 수 없이 P1이 먼저 CPU를 점유하게 된다.

<br/>

FCFS보다 효울성이 매우 높지만 그에 따른 단점도 존재한다.  
일단 가장 중요한 공평성에 어긋난다. 처리 시간이 긴 프로세스의 경우 처리 시간이 짧은 프로세스가 계속해서 들어온다면 대기 큐에서 영영 CPU를 할당받지 못할 수 있다. 이를 **starvation 현상**이라고 한다.  
그리고 중간에 입출력 버스트가 빈번하게 요구되는 프로세스의 경우 운영체제가 프로세스의 종료 시간을 정확하게 예측하기 어렵다.

<br/>

### HRN(Highest Response Ratio Next) 스케줄링
HRN 스케줄링은 SJF 스케줄링에서 발생할 수 있는 아사 현상을 해결하기 위해 만들어진 비선점형 알고리즘으로, 최고 응답률 우선 스케줄링이라고도 한다.  
SJF 스케줄링에 Aging 기법을 합친 비선점형 알고리즘이다.  
Aging이란 나이를 먹는다는 의미 그대로 starvation을 해결하기 위해 대기 시간이 길어지면 우선 순위를 높여주는 방법이다.

<br/>

SJF 스케줄링은 프로세스의 실행 시간이 판단 기준이기 때문에 항상 적은 시간을 사용하는 프로세스에 우선권이 주어지지만, HRN 스케줄링은 서비스를 받기 위해 기다린 시간과 CPU 사용 시간을 고려하여 스케줄링을 하는 방식이다. HRN 스케줄링에서 프로세스의 우선 순위를 결정하는 기준은 다음과 같다.  
- 우선 순위 = (대기 시간 + CPU 사용 시간) / CPU 사용 시간  

SJF와 마찬가지로 실행 시간이 적은 프로세스의 우선 순위가 높지만 대기 시간이 너무 길어지면 실행 시간이 길더라도 CPU를 할당받을 수 있다. 하지만 여전히 공평성이 말끔히 해결되지는 않는다.

<br/>

### 라운드 로빈(RR, Round Robin) 스케줄링
프로세스에게 각각 동일한 CPU 할당 시간(타임 슬라이스, quantum)을 부여해서 이 시간 동안만 CPU를 이용하게 한다. 만약 할당 시간 동안 처리를 다 하지 못하면 CPU를 빼앗고 다음 프로세스에게 넘긴다. 빼앗긴 프로세스는 준비 큐의 맨 뒤로 간다. 따라서 선점형 방식이다.  
따로 CPU 처리 시간을 계산하지 않아도 돼서 선점형 방식의 가장 단순하고 대표적인 방법이다. 우선 순위도 없기 때문에 매우 공평하다.

<br/>

라운드 로빈 알고리즘의 경우, 만약 할당 시간이 q고 대기 중인 프로세스가 n 개라면 어떤 프로세스도 (n - 1) q 이상을 기다리지 않아도 된다. 이는 곧 **모든 프로세스가 최초 응답 시간을 빠르게 보장받을 수 있다**는 큰 장점을 가지게 된다. 자연히 콘베이 효과 역시 줄어든다.

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bwsAyu/btqtYKVKWZO/zr8z1dwh0dcHjioiwhUMIK/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bwsAyu/btqtYKVKWZO/zr8z1dwh0dcHjioiwhUMIK/img.png)

<br/>

위의 경우 time quantum = 5인 경우다. 타임 퀀텀(타임 슬라이스)동안 처리를 다 하지 못한 P1은 CPU를 빼앗기고 대기 큐의 맨 뒤로 간 다음 P2에게 넘겨 준다. P2는 3ms만에 처리를 완료하고 바로 P3에게 CPU를 넘겨 준다.

<br/>

라운드 로빈 방식에서 가장 중요한 부분은 타임 슬라이스의 크기 결정이다.  
**타임 슬라이스가 큰 경우** 처리 시간이 긴 프로세스에 의해 CPU의 효율성이 떨어질 수 있다. 비디오 플레이어와 워드 프로세서를 동시에 실행했을 때 타임 슬라이스가 크다면 비디오가 약간씩 끊겨서 재생될 것이다. 그리고 만약 타임 슬라이스가 무한대로 설정되면 FCFS 스케줄링과 다를 바 없어진다.  
**타임 슬라이스가 작은 경우** 여러 프로그램이 동시에 실행되는 효과를 볼 수 있다. 하지만 너무 작으면 잦은 문맥 교환이 일어나 오버헤드가 상당히 커진다.  
때문에 적당한 타임 슬라이스를 설정하는 것이 중요하다. 보통 10-100 ms로 설정한다.

<br/>

### SRT(Shortest Remaining Time, SRTF(Shortest Remaining Time First) 스케줄링
SRT 스케줄링은 SJF 스케줄링과 라운드 로빈 스케줄링을 혼합한 방식으로, 최소 잔류 시간 우선 스케줄링이라고도 한다.  
쉽게 말해 SJF 스케줄링의 선점형 버전이라고 할 수 있다. 먼저 온 프로세스가 CPU를 할당받고 있더라도 남은 처리 시간이 뒤에 온 프로세스의 처리 시간보다 길면 CPU를 빼앗긴다.

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/ceeNYb/btqtYLAlP1i/J1q8Bp7y8qorIE4d7yttQk/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/ceeNYb/btqtYLAlP1i/J1q8Bp7y8qorIE4d7yttQk/img.png)

<br/>

어떤 알고리즘보다 평균 대기 시간이 가장 짧은 알고리즘이다.  
하지만 이 방식은 기본적으로 선점형 방식이기 때문에 잦은 문맥 교환이 일어나고 그에 따른 오버헤드가 커진다. 그리고 starvation 현상이 더 심각하게 발생할 수 있다.  
또한 CPU의 예상 시간을 예측하기가 너무 힘들기 때문에 실제로 사용되기가 매우 어렵다. (exponential averaging을 통해 예측을 할 수는 있다.)

<br/>

### 우선 순위(Priority) 스케줄링
프로세스의 중요도에 따라 매긴 우선순위를 반영한 알고리즘으로 위에서 알아본 SJF, HRN, SRTF도 우선순위 스케줄링 알고리즘의 일종이다.  
위의 알고리즘들의 문제점과 마찬가지로 starvation 문제와 공평성 문제가 있다.

<br/>

- 각각의 프로세스에 우선 순위 넘버가 있다.
- 가장 높은 우선순위의 프로세스에 CPU를 할당한다.
- 선점형과 비선점형이 나뉜다.
- SJF도 Priority 스케줄링이라고 할 수 있다. (다음 CPU burst time이 우선순위인 것처럼 작동하므로)
- 기아(Starvation) 문제가 발생할 수 있다. 기아 문제란 낮은 우선순위의 프로세스가 절대 실행되지 않는 문제를 뜻한다.
- 기아 문제를 해결하기 위해서 노화(aging)를 사용할 수 있다. 시간이 지날수록 프로세스의 우선순위를 높여주는 식이다.

<br/>

- Priority 스케줄링 예시

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/A4IZf/btrwVrs2Cux/s1k5EWSxBkYRMgULlr4F70/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/A4IZf/btrwVrs2Cux/s1k5EWSxBkYRMgULlr4F70/img.png)

<br/>

모두 0초에 도착했다고 했을 때, 우선 순위에 따라 위와 같이 처리된다.

<br/>

### 다단계 큐(Multilevel Queue) 스케줄링
다단계 큐 스케줄링은 우선순위에 따라 준비 큐를 여러 개 사용하는 방식이다. 당연히 우선 순위가 높은 큐에 먼저 CPU가 할당되어 큐에 속한 모든 프로세스가 처리되어야 다음 우선 순위 큐가 실행될 수 있다. 그리고 한 번 우선 순위가 매겨저 준비 큐에 들어가면 이 우선 순위는 바뀌지 않는다.  
각 큐 사이에서 프로세스들이 이동할 수 없다.

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/LqYAc/btqtW0lcMXw/kM2ex6H9lu5f2tSfjoRgvK/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/LqYAc/btqtW0lcMXw/kM2ex6H9lu5f2tSfjoRgvK/img.png)

<br/>

각 큐는 독립적인 스케줄링 알고리즘을 가질 수 있는데, 보통 전면 프로세스들이 속해있는 큐는 우선 순위도 높고 라운드 로빈 스케줄링을 사용해 타임 슬라이스를 작게 한다.  
후면 프로세스에는 사용자와의 상호작용이 없으므로 가장 간단한 FCFS 방식으로 처리한다. 보통 총 CPU 시간이 전면 프로세스의 처리에 80%, 후면 프로세스 처리에 20%가 할당된다.  
이 다단계 큐 알고리즘 역시 문제는 starvation 현상과 공평성 문제다.

<br/>

### 다단계 피드백 큐(Multilevel Feedback Queue) 스케줄링
다단계 큐의 공평성 문제를 완화하기 위해 신분 하락이 가능한 알고리즘이다. 이 알고리즘에서는 우선 순위가 변동되기 때문에 큐 사이의 이동이 가능하다.  
한 번 CPU를 할당받은 프로세스는 우선 순위가 조금 낮아진다. 따라서 더 낮은 큐로 이동하게 된다. (우선 순위가 높아져 상위 큐로 이동할 수도 있다.)  
그리고 더 보완하기 위해 우선 순위가 높은 큐보다 우선 순위가 낮은 큐에 타임 슬라이스 크기를 크게 준다. 어렵게 얻은 CPU를 좀 더 오랫동안 사용하게 해 주기 위함이다.

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bt1O9K/btqtWHGcTpB/3OHZNOKR4XRoBV8njb5Gjk/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bt1O9K/btqtWHGcTpB/3OHZNOKR4XRoBV8njb5Gjk/img.png)

<br/>
<br/>

# 🗣 면접 예상 질문
## Q1. 스케줄링은 무엇이고, CPU 스케줄링은 언제 발생하는지 설명해 주세요.
여러 프로세스가 있고, 이 프로세스들이 자원(CPU 등)을 동시에 요구하는데 자원은 제한되어 있다. 그럴 때 제한된 자원들을 어떻게(순서를 할당하는 등) 나눠줄 것인지에 대한 정책을 스케줄링이라고 말한다.  
CPU 스케줄링은 다음과 같은 상황에 발생한다.  
- 실행 상태에서 대기 상태로 전환될 때 (ex : 입출력 요청) - Non preemptive(비선점)
- 실행 상태에서 준비 상태로 전환될 때 (ex : 인터럽트 발생) - preemptive(선점)
- 대기 상태에서 준비 상태로 전환될 때(ex : 입출력이 종료될 때)
- 종료될 때(Terminated)

<br/>
<br/>

## Q2. 스케줄링은 어떻게 분류하나요?
CPU 스케줄링은 규모에 따라 장기, 중기, 단기 스케줄링으로 구분된다.

<br/>

1. 장기 스케줄링(Long-term scheduler)
- 가장 큰 틀에서 이루어지는 CPU 스케줄링이다. 고수준 스케줄링, 작업 스케줄링이라고도 한다.
- 프로세스에 Memory(및 각종 자원)을 주는 문제를 스케줄링 한다.
- 전체 시스템의 부하를 고려하여 작업 요청을 받아들일지, 거부할지에 대한 결정을 한다. 즉, new 상태의 프로세스를 admitted 하는 작업을 장기 스케줄러가 한다.
- 즉, 장기 스케줄링의 결정에 따라 시스템 내의 프로세스 총 개수(degree of multiprogramming)가 정해진다.
- 최근 운영체제에서는 보통 장기 스케줄러가 없다. 프로그램을 실행시키면 곧바로 ready 상태에 돌입한다.

<br/>

2. 중기 스케줄링(Medium-term scheduler, Swapper)
- 장기 스케줄링은 프로세스의 활성화 승인을 다룬다면 중기 스케줄링은 이미 활성화가 된 프로세스들에 대한 관리를 한다.
- 시스템의 과부하를 막기 위해 활성화된 프로세스들의 중지 여부를 결정하여 활성화된 프로세스 수를 조절한다.
- 즉, 여유 공간 마련을 위해 프로세스를 통째로 메모리에서 디스크로 쫓아낸다.(Swap out)
- 이 역시 degree of multiprogramming을 제어하는 것이다.
- 중기 스케줄링에 의해 중지된 프로세스들은 보류 상태(Suspended, Stopped)가 된다.

<br/>

3. 단기 스케줄링 (Short-term scheduler, CPU scheduler)
- 가장 작은 단위의 스케줄링을 단기 스케줄링이라고 한다.
- 어떤 프로세스에 CPU를 할당할지, 어떤 프로세스를 대기 상태로 보낼지 등을 결정한다.
- 단기 스케줄러가어떤 기준에 따라 프로세스를 선택(스케줄링 알고리즘)하고 어느 정도 자원을 배분(Time slice와 관련)할지에 따라 시스템에 큰 영향을 끼친다.
- 단기 스케줄링은 스케줄링 중에서도 핵심인 부분이라 뒤에서 다룰 내용은 대부분 단기 스케줄링에 대한 내용이다.

<br/>
<br/>

## Q3. 전면 프로세스와 후면 프로세스에 대해 설명해 주세요.
**전면 프로세스**란 GUI를 사용하는 OS에서 화면 맨 앞에 놓인 프로세스를 말한다.  
사용자와 상호작용이 있는 프로세스이다.  
사용자 측면에서는 입출력이 중요하기에 사용자 측면에서는 대기 시간, 응답 시간, 반환 시간을 줄여 줄 수 있는 스케줄링을 활용해야 한다.

<br/>

**후면 프로세스**란 사용자와 상호작용이 없는 프로세스이다.  
시스템 측면에서는 시스템의 자원을 최대한 활용할 수 있는 처리량 + CPU 사용률을 높게 해 주는 스케줄링을 활용해야 한다.  
어떠한 상호 작용 없이 순수 로직을 처리하는 프로세스를 의미한다.

<br/>
<br/>

# 🗂 참고
- [[운영체제] CPU 스케줄링 알고리즘 정리 및 요약 | FCFS, SJF, Round Robin (tistory.com)](https://code-lab1.tistory.com/45)
- [[운영체제] CPU 스케줄링 (tistory.com)](https://steady-coding.tistory.com/509)
- [CPU 스케줄링 (tistory.com)](https://bnzn2426.tistory.com/65)
- [[OS] CPU 스케줄링(CPU-Scheduling) (velog.io)](https://velog.io/@yu-jin-song/OS-CPU-%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81CPU-Scheduling)
- [[Operating System - Chapter 5] CPU 스케줄링 (imbf.github.io)](https://imbf.github.io/computer-science(cs)/2020/10/18/CPU-Scheduling.html)
- [[운영체제] 스케줄링 관련 면접 질문 대비 (tistory.com)](https://deious.tistory.com/290)
- [운영체제 면접 (velog.io)](https://velog.io/@twan/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EB%A9%B4%EC%A0%91)
- [책] 쉽게 배우는 운영체제
