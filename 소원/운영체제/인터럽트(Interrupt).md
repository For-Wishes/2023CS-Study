# 인터럽트

> CPU가 프로그램을 실행하고 있을 때, 입출력 하드웨어 등의 장치에 예외상황이 발생하여 처리가 필요할 경우에 CPU에게 알려 처리할 수 있도록 하는 것
> 

## 하드웨어 인터럽트

- CPU 외부의 디스크 컨트롤러나 주변장치로부터 요구되는 것으로, 운영체제의 처리를 요하는 상황을 알리기 위해 전기적인 신호를 사용해 구현

### Maskable Interrupt

- Interrupt Mask(인터럽트가 발생했을 때 요구를 받아들일지 말지 지정하는 것) 가능
- 프로그램이 마이크로프로세서의 주의를 100% 필요로 하는 동안 일시적으로 기능이 저지(mask)될 수 있는 것

### Non-maskable Interrupt

- Interrupt Mask에 영향을 받지 않는 가장 우선순위가 높은 인터럽트.
- 하드웨어 인터럽트의 일종으로, 소프트웨어나 키보드 등 하드웨어 장치에 의해서 생성되는 인터럽트 요구를 우회하고 그것들보다 우선 순위를 가짐
- 다른 어떤 서비스 기억 장치 오류나 정전 사태와 같은 급박한 상황에서만 마스크 불가능 인터럽트 요구가 마이크로프로세서에 하달
- Interrupt Mask가 불가능
- **거부, 무시할 수 없음**
- 정전, 하드웨어 고장 등 어쩔 수 없는 오류

### 하드웨어 인터럽트 종류

- 입출력 인터럽트(I/O Interrupt): 입출력 작업의 종료나 입출력 오류에 의해 CPU의 기능이 요청됨
- 정전, 전원 이상 인터럽트(Power  fail Interrupt): 전원 공급의 이상
- 기계 착오 인터럽트(Machine Check Interrupt): CPU의 기능적인 오류
- 외부 신호 인터럽트(External Interrupt): I/O 장치가 아닌 오퍼레이터나 타이머에 의해 의도적으로 프로그램이 중단된 경우

## 소프트웨어 인터럽트

- 외부가 아닌 CPU 내부에서 자신이 실행한 명령이나 CPU의 명령 실행에 관련된 모듈이 변화하는 경우 발생
- 프로그램 실행 중 프로그램상의 처리 불가능한 오류나 이벤트를 알리기 위한 경우 발생
    - 트랩(Trap) 또는 예외(Exception)이라 부름
- 프로그램 오류에 의해 생기는 인터럽트
- 프로그램 내에서 특별한 서비스를 요구하거나 감시를 목적으로 의도적으로 프로그램이 발생시킨 특별한 명령어에 의해 발생되기도 한다

### 소프트웨어 인터럽트 종류

- 예외 상황
    - 프로그램이 허용되지 않은 연산을 수행하려 할 때, 자동적으로 발생
    - 프로그램 검사 인터럽트(Program check interrupt)
        - 0으로 나누는 경우
        - OverFlow / UnderFlow
        - 페이지의 부재
        - 부당한 기억장소의 참조 등
    - 운영체제는 예외 상황이 발생했을 때, CPU의 제어권을 획득해 이 상황에 대한 조치를 취한다
- System  Call
    - 운영체제가 제공하는 서비스에 대한 프로그래밍 인터페이스 → System call
    - System call을 실행시키기 위한 CPU 명령어→ Supervier Call
    - 사용자 프로세스가 운영 체제의 서비스를 요청하기 위해 커널의 함수를 호출하는 것
    - 사용자 프로세스가 직접 특권 명령을 수행할 수 없으므로 시스템 콜 사용

### 인터럽트와 시스템 콜의 차이점

- 시스템 콜이나 예외 상황은 모두 사용자 프로세스로부터 CPU의 제어권이 운영체제에게 이양되어 처리되는데, 이 과정에 인터럽트 라인을 세팅하여 인터럽트를 발생시킨 후 제어권이 넘어가게 되므로 이들도 넓은 의미에서는 인터럽트의 범주에 포함 시킴
- 단지 인터럽트를 발생시키는 주체가 하드웨어 장치가 아닌 소프트웨어 이므로 소프트웨어 인터럽트라고 부름
- 대체로 하드웨어 인터럽트를 인터럽트라고 부른다

## 인터럽트 우선 순위

> 전원 이상 > 기계 고장 > 외부 신호 > 프로그램 인터럽트 > SVC
> 
- 일반적으로 하드웨어 인터럽트가 소프트웨어 인터럽트보다 우선순위가 높음

![image.png](https://blog.kakaocdn.net/dn/bXN8JO/btrcrNOCdrX/p9yBaxaFeCQKL7VleUPKWk/img.png)
## 인터럽트 처리 과정

![img1.daumcdn.png](https://blog.kakaocdn.net/dn/bpgPHt/btq5NcPlGTH/BRIMZzBQQMUDm6ojSqgK00/img.png)
![img1.daumcdn.png](https://blog.kakaocdn.net/dn/9h8PF/btq5L4qJsN9/J1dii0rfe0jqtRen1IaNS0/img.png)
1. 명령어 실행 단계를 마칠 때마다 중앙처리장치는 반복적으로 인터럽트 요청이 있는지 확인하고 인터럽트가 발생하면
2. 프로그램 수행 중단
    - 현재 진행중인 기계어 코드 완료
    - 현재 수행중인 명령의 완료된 시점에서 중단
        - 현재의 주기억장치 사이클이 끝나는 시점이 아님
3. CPU의 특수 레지스터 중, 하이드로 인터럽트 마스크 비트를 보고 마스크 되면 인터럽트 무시
4. 인터럽트 벡터 읽어 ISR(인터럽트 서비스  루틴) 주소값을 얻는다
5. ISR로 점프
    - PC(Program Counter, IP)에 기억되어 있는 주소를 안전한 곳에 기억시켜서 보존
6. 현재 진행중인 프로그램의 레지스터 대피
7. 인터럽트 전처리 실행
    - 원인 판단
    - 처리 루틴(Intrrupt Processing Routine) 호출
8. 인터럽트 처리 루틴 수행
9. 해당 일을 다 처리하면, 대피시킨 레지스터 복원
10. ISR의 끝에 IRET 명령어에 의해 인터럽트 해제
11. IRET 명령어가 실행되면, 대피시킨 PC 값을 복원하여 이전 실행 위치로 복원

> PC의 값을 안전한 곳에 기억시켜 보존 → 원인 판단 → IRP의 수행
> 

### 인터럽트 벡터

- 여러가지 인터럽트에 대해 해당 인터럽트 발생시 처리해야 할 루틴(ISR)의 주소를 보관하고 있는 공간
- 인터럽트 벡터 테이블: 주기억장치의 특정 영역에 여러 개의 인터럽트 벡터를 모아놓은 영역
- 대부분의 CPU는 인터럽트 벡터 테이블을 가지고 있다

### ISR

- 인터럽트 서비스 루틴, 인터럽트 핸들러
- 인터럽트가 접수되면 각각의 인터럽트에 대응하여 특정 기능을 처리하는 기계어 코드 루틴
- 실행중이던 레지스터와 PC를 보관함으로써 CPU의 상태 보존
- 인터럽트가 핸들링이 완료되면 이전의 상태로 복귀

### 폴링

- 사용자가 명령어를 사용해 입력 핀의 값을 계속 읽어 변화를 알아내는 방식
- 인터럽트 요청 플래그를 차례로 비교하여 우선순위가 가장 높은 인터럽트 자원을 찾아 이에 맞는 인터럽트 서비스 루틴 수행
- 만약 인터럽트 기능이 없었다면 컨트롤러는 특정한 어떤 일을 할 시기를 알기 위해 계속 체크함
- 폴링을 하는 시간에는 원래 하던 일에 집중할 수가 없게 되어 많은 기능을 수행하지 못하는 단점
- 하드웨어에 비해 속도가 느림

### 인터럽트 방식

- MCU(마이크로 컨트롤러) 자체가 하드웨어적으로 변화를 체크하여 변화시에만 일정한 동작을 하는 방식
- 인터럽트 방식은 하드웨어로 지원을 받아야 하는 제약이 있지만, 폴링에 비해 신속하게 대응가능
- 실시간 대응이 필요할 때 필수적인 기능
- 인터럽트는 발생시키를 예측하기 힘든 경우에 컨트롤러가 가장 빠르게 대응할 수 있는 방법

# 질문

### 폴링과 인터럽트의 차이

- 폴링: 대상을 주기적으로 감시하여 상황이 발생하면 해당 처리 루틴을 실행해 처리
- 인터럽트: 상대가 마이크로프로세서에게 일을 처리해달라고 요청하는 수단
- 인터럽트 방식은 하드웨어로 지원을 받아야 하는 제약이 있지만, 폴링에 비해 신속하게 대응하는 것이 가능 따라서 실시간 대응이 필요할 때는 필수적인 기능

### 인터럽트와 트랩의 차이점

- 인터럽트: 하드웨어적 흐름의 변화로, 프로그램의 외부(I/O 장치, 디스크 등)에서 발생하며, 발생 시점이 일정하지 않기 떄문에 비동기적
- 트랩: 소프트웨어적 흐름의 변화로 소프트웨어 인터럽트라고도 한다. 프로그램 내부에서 일어나며 발생 시점이 일정한 지점이기 때문에 동기적(고정된 영역에서 일어남)

**참고**

[[OS] Interrupt 인터럽트란?](https://doh-an.tistory.com/31)

[TTA정보통신용어사전](http://terms.tta.or.kr/dictionary/dictionaryView.do?subject=마스크+불가능+인터럽트)

[소프트웨어와 하드웨어 - 인터럽트란?](https://huistorage.tistory.com/111)

[[OS] 인터럽트, Interrupt](https://velog.io/@nnnyeong/OS-인터럽트-Interrupt)

[인터럽트(Interrupt)의 종류와 처리과정](https://oizys.tistory.com/4)

[인터럽트 처리과정 및 정의, 종류 알아보기](https://mindstation.tistory.com/164)

[인터럽트(Interrupt)](https://gyeong-log.tistory.com/63)

[인터럽트(Interrupt) | 👨🏻‍💻 Tech Interview](https://gyoogle.dev/blog/computer-science/operating-system/Interrupt.html)

[인터럽트(Interrupt)](https://gyeong-log.tistory.com/63)
