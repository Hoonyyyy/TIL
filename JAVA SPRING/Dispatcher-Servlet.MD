# Dispatcher-Servlet

- 디스패처 서블릿의 dispatch는 "보내다" 라는 뜻을 가지고 있다.
- 이러한 단어를 포함하는 디스패처 서블릿은 HTTP 프로토콜로 들어오는 모든 요청을 가장 먼저 받아
- 적합한 컨트롤러에게 위임해주는 프론트 컨트롤러(Front Controlloer)라고 정의할 수 있다.

```
자세히 설명

클라이언트로부터 어떠한 요청이 오면 Tomcat(톰캣)과 같은 서블릿 컨테이너가 요청을 받게 된다.
그리고 이 모든 요청을 프론트 컨트롤러인 디스패처 서블릿이 가장 먼저 받게 된다.
그러면 디스패처 서블릿은 공통적인 작업을 먼저 처리한 후에 해당 요청을 처리해야 한느 컨트롤러를 찾아서 작업을 위임한다.

여기서 Front Controlloer(프론트 컨트롤러)라는 용어가 사용되는데, Front Controller는 주로 서블릿 컨테이너의 제일 앞에서
서버로 들어오는 클라이언트의 모든 요청을 받아서 처리해주는 컨트롤러로써, MVC구조에서 함꼐 사용되는 디자인 패턴이다.
```


### 장점
- 과거에는 모든 서블릿을 URL 매핑을 위해 web.xml에 모두 등록해주어야만 했으나,
- dispatcher-servlet이 해당 어플리케이션으로 들어오는 모든 요청을 핸들링해주고 공통 작업을 처리하면서
- 상당히 편리하게 이용할 수 있게 되었다.
- 우리가 컨트롤러를 구현하기만 하면 디스패치 서블릿이 알아서 적합한 컨트롤러로 위임해주는 구조가 되었다.

### Dispatcher-servlet의 구조

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbImFbg%2FbtrGzZMTuu2%2FCkY4MiKvl5ivUJPoc5I3zk%2Fimg.png">

1. 클라이언트의 요청을 디스패처 서블릿이 받음
2. 요청 정보를 통해 요청을 위임할 컨트롤러를 찾음
3. 요청을 컨트롤러로 위임할 핸들러 어댑터를 찾아서 전달함
4. 핸들러 어댑터가 컨트롤러로 요청을 위임함
5. 비지니스 로직을 처리함
6. 컨트롤러가 반환값을 반환함
7. 핸들러 어댑터가 반환값을 처리함
8. 서버의 응답을 클라이언트로 반환

### 디스패처 서블릿을 통해 요청을 처리할 컨트롤러를 찾아서 위임하고, 그 결과를 받아옴 정도로 정리가 


<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoN96r%2Fbtrw7SYEpgr%2FlKLp5nqEZUJR32GoPc9bwk%2Fimg.png">
