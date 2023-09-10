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
- 



출처

https://boradol0902.tistory.com/35
