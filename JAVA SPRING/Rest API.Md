# Rest API

### Rest (Representational State Transfer)
- HTTP URI를 통해 리소스를 명시하고 HTTP Method(GET, POST, DELETE, PUT)을 사용하여 리소스에 대한 행위 표현

### API (Application Programming Interface)
- 응용프로그램에서 사용할 수 있도록 운영체제나 프로그래밍 언어가 제공하는 기능을 제어도록 만들어둔 인터페이스


### 합치기
- URI와 HTTP Method를 이용하여 외부에서 만들어둔 기능들을 제어하는 것


### 일반적인 통신과정
```
            
            요청(Http Method)
클라이언트         ----->        서버

                <-----
           응답 (Code, Data)
```


## 스프링은 클라이언트와 서버 중 "서버" 이다.
- Rest API 구조에서는 뷰와 관련된 처리가 없어지고, 사용자에게 데이터만 응답한다.
- 어노테이션에서는 MVC구조를 위해 컨트롤러가 구현된 클래스에서 사용되는 어노테이션은 @Controlloer인데
- Result API를 위한 어노테이션은 @RestController이다.
- @RestController = @Controller + @ResponseBody


### 비동기 / Jquery / Ajax
- 클라이언트에서 서버에 요청을 보낼때 MVC구조에서는 form태그를 사용했지만
- RestAPI 구조에서는 Ajax를 통한 비동기 처리르한다.
- 비동기 처리의 대표적인것이 Ajax


