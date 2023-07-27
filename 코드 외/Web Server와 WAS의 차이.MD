# Web Server와 WAS의 차이


<img src="https://gmlwjd9405.github.io/images/web/static-vs-dynamic.png">

## Static Pages
- Web Server는 파일 경로 이름을 받아 경로와 일치하는 file contents를 반환함
- 항상 동일한 페이지를 반환함 ( 정적인 컨텐츠 제공 )
- ex) image, html, css, javascript 파일과 같은 컴퓨터에 저장되어 있는 파일들
- http프로토콜 기반으로 하여 클라이언트(웹 브라우저 또는 웹 크롤러)의 요청을 서비스 하는 기능을 담당
- 기능 1)
- 정적인 컨텐츠 제공
- WAS 거치지 않고 바로 자원을 제공
- 기능 2)
- 동적인 컨텐츠 제공을 위한 요청 전달
- 클라이언트 요청(Request)을 WAS에 보내고, WAS가 처리한 결과를 클라이언트에게 전달(응답, Response)함
- 클라이언트는 일반적으로 웹 브라우저를 의미함

## Dynamic Pages
- 인자의 내용에 맞게 동적인 contents를 반환함
- DB 조회나 다양한 로직 처리를 요구하는 동적인 컨텐츠를 제공하기 위해 만들어진 Application Server
- HTTP를 통해 컴퓨터나 장치에 어플리케이션을 수행해주는 것
- 웹 컨테이너(Web Container) 혹은 서블릿 컨테이너(Servlet Container) 라고 불린다.
- WAS = Web Server + Web Container
- Web Server 기능들을 구조적으로 분리하여 처리하고자하는 목적으로 제시됨
  - 분산 트랜잭션, 보안, 메시징, 쓰레드 처리 등의 기능을 처리하는 분산 환경에서 사용됨
  - 주로 DB서버와 같이 수행됨
  - 예) Tomcat, JBoss, Jeus 등


## Web Server가 필요한 이유?
- Web Server를 통해 정적인 파일들을 Application Server까지 가지 않고 앞단에서 빠르게 보내줌
- 따라서 Web Server에서는 정적 컨텐츠만 처리하도록 기능을 분배하여 서버의 부담 줄임

## WAS가 필요한 이유?
- 웝 페이지는 정적 컨텐츠와 동적 컨텐츠가 모두 존재함
  - 사용자의 요청에 맞게 적절한 동적 컨텐츠를 만들어 제공함
  - 이떄, Web Server만을 이용하면 사용자가 원하는 요청에 대한 결과값을 모두 미리 만들어야함...
  - 이렇게 하기엔 자원이 절대적으로 부족함
- 따라서 WAS를 통해 요청에 맞는 데이터를 DB에서 가져와서 비즈니스 로직에 맞게 그때 그때
- 결과를 만들어서 제공함으로써 자원을 효율적으로 사용

## WAS가 다 하면 되는거 아니야? ( 이렇게 생각하면 큰일남 )
- 기능을 분리하여 서버 부하 방지
```
WAS는 DB 조회나 다양한 로직을 처리하느라 바쁘다.
그렇기에 단순한 정적 컨텐츠는 Web Server에서 빠르게 클라이언트에 제공하는 것이 좋음

WAS는 기본적으로 동적 컨텐츠를 제공하기 위해 존재하는 서버

만약 정적 컨텐츠 요청까지 WAS가 처리하면 정적 데이터 처리로 인해 부하가 커지게 되고,
동적 컨텐츠의 처리가 지연됨에 따라 수행 속도 느려짐

페이지 노출시간 늘어남
```
- 물리적으로 분리하여 보안강화
  - SSL에 대한 암복호화 처리에 Web Server를 사용
- 여러 대의 WAS를 연결 가능
- 자원 이용의 효율성 및 장애 극복, 배포 및 유지보수의 편의성을 위해 Web Server와 WAS를 분리함


## Web Service Architecture
<img src="https://gmlwjd9405.github.io/images/web/web-service-architecture.png">
1. df
2. df



