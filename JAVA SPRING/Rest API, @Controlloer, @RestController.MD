# Rest API, @Controlloer, @RestController

### Rest (Representational State Transfer)
- HTTP URI를 통해 리소스를 명시하고 HTTP Method(GET, POST, DELETE, PUT)을 사용하여 리소스에 대한 행위 표현

### API (Application Programming Interface)
- 응용프로그램에서 사용할 수 있도록 운영체제나 프로그래밍 언어가 제공하는 기능을 제어도록 만들어둔 인터페이스
- 한 프로그램에서 다른 프로그램으로 데이터 주고받기 위한 방법
```
API는 식당 메뉴판 (ex 파스타.피자.식전빵)
- 식당과 손님이 주고받기위한것

웹툰 보내주는프로그램(웹서버)
웹툰서비스 API : 웹툰서버와 손님이 웹툰을 주고받기 위한 방법( 여기서 방법은 코드 )

유저도 Get요청하는 코드짜야 웹툰 볼 수 있음

public API : 누구나 사용가능한 공개API
private API : 사내에서 몰래쓰는 API
partner API : 미리 정해놓은 사람만 쓰는 API
```


### 합치기
- URI와 HTTP Method를 이용하여 외부에서 만들어둔 기능들을 제어하는 것
- 여기서 외부란?
- 웹 서비스를 제공하거나 서버나 시스템 등을 사용자나 클라이언트가 접근하는 위치를 의미함
- 외부에서는 정의된 URI와 HTTP 메소드를 통해 서버에 요청을 보내고, 해당 요청에 따라 기능들을 수행하고 그 결과를 반환받을 수 있다.
- 사용은 웹에서 클라이언트가 서버에 요청할때 쓰임

### 일반적인 통신과정
```
            
            요청(Http Method)
클라이언트         ----->        서버

                <-----
           응답 (Code, Data)
```


## 스프링은 클라이언트와 서버 중 "서버" 이다.
- Rest API 구조에서는 뷰와 관련된 처리가 없어지고, 사용자에게 데이터만 응답한다.
- 어노테이션에서는 MVC구조를 위해 컨트롤러가 구현된 클래스에서 사용되는 어노테이션은 @Controller인데
- Result API를 위한 어노테이션은 @RestController이다.
- @RestController = @Controller + @ResponseBody


### 비동기 / Jquery / Ajax
- 클라이언트에서 서버에 요청을 보낼때 MVC구조에서는 form태그를 사용했지만
- RestAPI 구조에서는 Ajax를 통한 비동기 처리르한다.
- 비동기 처리의 대표적인것이 Ajax



## @Controller
- 주로 view 반환할떄 사용

## @RestController
- 주로 Data를 JSON형태로 반환할떄 사용함


