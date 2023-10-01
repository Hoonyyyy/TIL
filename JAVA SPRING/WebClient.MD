# WebClient
# 더 정리하기


- spring5에서 등장한 HTTP 클라이언트 라이브러리
- 여기서 말하는 HTTP 클라이언트라고 하는 것은 HTTP 프로토콜을 이용하여 서버와 통신하는 것을 의미하며 다른 말로는 서버에 API 요청을 보내는 주체
- webClient가 등장하기 이전까지는 spring에서 자주 사용되던 HTTP 클라이언트는 restTemplate가 존재했음
- 스프링에서 지금은 webClient 권장
- 장점
  - 비동기적으로 요청하는 non-blocking 처리 방식
  - 요청을 보내고 응답을 받을 때까지 대기하지 않기 때문에 처리 속도가 빠름
  - 비동기 처리 방식으로 인해 대용량 처리를 할 때 용이함

출처

https://jforj.tistory.com/319
