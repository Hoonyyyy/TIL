# 용어정리(IDLE,READY 등)
- Stack, Queue 관련 글 작성하다보니 Idle, Idle 하는데 이게 뭐지?? 하다가 정리하게 됐다
- 일단 IDLE = "프로세스가 실행하고 있지 않은 상태"
- 프로세스 : 동작중인 프로그램, 운영체제가 관리하는 실행 단위
- I/O 인터럽트 대기중, 준비 큐에서 대기, sleep하거나
- 이 상태에서 전원을 절약
- 밑에서는 프로세스의 상태를 나타내는 용어를 더 봄


<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdb4jvG%2FbtqHbZzUZF6%2FqdUFFymh3JJhqjPXbIyuV0%2Fimg.png">

#### IDLE
- 프로그램을 수행하지 않는 상태(프로세스가 아님)

#### READY
- 대기상태, 스케쥴러에 의해 자신의 순서를 대기하고 있는 상태

#### RUN
- 실행 상태
- CPU를 사용 중인 상태
- CPU 사용이 끝나면 READY 상태로 전이
- 비정상적인 작업으로 SUSPENDED 상태로 전이
- 모든 작업이 끝나면 IDLE 상태로 전이
- 입출력 요청이 오면 BLOCK 상태로 전이

#### BLOCK
- 요청한 입출력 수행 완료를 기다리는 상태
- 입출력 수행을 완료하면 READY 상태로 전이(Wake Up)
- 입출력 수행에 지연이 발생하면 SLEEP 상태로 전이

#### SLEEP
- 입출력 수행에 지연이 발생하는 상태
- 입출력 수행을 완료하면 READY 상태로 전이
- SLEEP 상태가 특정 시간동안 지속하면 SWAP 상태로 전이

#### SWAP
- SLEEP 상태를 지속하여 우선적으로 SWAP 대상인 상태
- 입출력 수행을 완료하면 READY 상태로 전이

#### SUSPENDED
- 비정상적인 요청으로더 이상 작업을 수행할 수 없는 상태

### PCB(Process Control Block)
- 프로세스의 제어 정보를 저장해 놓는 영역을 말한다.
- 프로세스의 상태, 프로세스 ID, CPU 레지스터 정보, ACCOUNTER 정보 등으로 구성한다.

### 스레드
- 프로세스 환경에서 독립적으로 수행 가능한 작업 단위
- 윈도우즈 운영체제처럼 스레드가 스케쥴링 단위인 시스템도 존재한다.



출처

https://boradol0902.tistory.com/35
