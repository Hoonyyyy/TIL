# Dispatcher-Servlet

- 디스패처 서블릿의 dispatch는 "보내다" 라는 뜻을 가지고 있다.
- 이러한 단어를 포함하는 디스패처 서블릿은 HTTP 프로토콜로 들어오는 모든 요청을 가장 먼저 받아
- 적합한 컨트롤러에게 위임해주는 프론트 컨트롤러(Front Controlloer)라고 정의할 수 있다.

```
자세히 설명

클라이언트로부터 어떠한 요청이 오면 Tomcat(톰캣)과 같은 서블릿 컨테이너가 요청을 받게 된다.
그리고 이 모든 요청을 프론트 컨트롤러인 디스패처 서블릿이 가장 먼저 받게 된다.
그러면 디스패처 서블릿은 공통적인 작업을 먼저 처리한 후에 해당 요청을 처리해야 하 컨트롤러를 찾아서 작업을 위임한다.

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

### 디스패처 서블릿을 통해 요청을 처리할 컨트롤러를 찾아서 위임하고, 그 결과를 받아옴 정도로 정리가 됨



### 1. 클라이언트의 요청을 디스패처 서블릿이 받음
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoN96r%2Fbtrw7SYEpgr%2FlKLp5nqEZUJR32GoPc9bwk%2Fimg.png">

### 2. 요청 정보를 통해 요청을 위임할 컨트롤러를 찾음
```
가장 먼저 어느 컨트롤러가 요청을 처리할 수 있는지 식별해야 하는데 이 역할을 하는것이 HandlerMapping

최근(22년도) @Controlloer에 @RequestMapping 관련 어노테이션을 사용해 컨트롤러를 작성하는 것이 일반적이다.
하지만 예전 스펙에 따라 Controller 인터페이스를 구현하여 컨트롤러를 작성할 수도 있다.
즉, 컨트롤러를 구현하는 방법이 다양하기 때문에 스프링은 HandlerMapping 인터페이스를 만들어두고, 다양한 구현 방법에 따라 요청을 처리할
대상을 찾도록 되어있다.

오늘날 흔한 @controller 방식은 RequestMappingHandlerMapping가 처리한다.
이는 @Controller로 작성된 모든 컨트롤러를 찾고 파싱하여 HashMap으로 <요청 정보, 처리할 대상> 괸라한다. 여기서 처리할 대상은 HandlerMethod
객체로 컨트롤러, 메서드 등을 갖고 있는데, 이는 스프링이 리플렉션을 이용해 요청을 위임하기 떄문이다.

그래서 요청이 들어오면 (Http Method, URI) 등을 사용해 요청 정보를 만들고, HashMap에서 요청을 처리할 대상(HandlerMethod)를 찾은 후에
HandlerExecutionChain으로 감싸서 반환한다. HandlerExecutionChain으로 감싸는 이유는 컨트롤러로 요청을 넘겨주기 전에 처리해야 하는
인터셉터 등을 포함하기 위해서이다.

```

### 3. 요청을 컨트롤러로 위임할 핸들러 어댑터를 찾아서 전달함
```
컨트롤러 요청을 위임은 디스패치 서블릿이 직접하는것이 아니라 Handler Adapter를 통해 위임한다.
컨트롤러로의 구현 방식이 다양하기에 구현 방식에 상관없이 요청을 위임할 수 있다.
```

### 4. 핸들러 어댑터가 컨트롤러로 요청을 위임 함
- [직렬화](https://github.com/Hoonyyyy/TIL/blob/main/JAVA/%EC%A7%81%EB%A0%AC%ED%99%94.MD#%EC%A7%81%EB%A0%AC%ED%99%94)
- [리플렉션](https://github.com/Hoonyyyy/TIL/blob/main/JAVA/%EB%A6%AC%ED%94%8C%EB%A0%89%EC%85%98(reflection).MD#%EB%A6%AC%ED%94%8C%EB%A0%89%EC%85%98reflection)
```
핸들러 어댑터가 컨트롤러로 요청을 위임한 전/후에 공통적인 전/후 처리 과정이 필요하다.
대표적인 인터셉터들을 포함해 요청 시에 @RequstParam, @requestBody 등을 처리하기 위한 ArgumnetResolver들과 응답 시에
ResponseEntity의 Body를 Json으로 직렬화한 등의 처리를 하는 ReturnValueHandler 등이 핸들러 어댑터에서 처리된다.
ArgumentResolver 등을 통해 파라미터가 준비되면 리플렉션 이용해 컨트롤러로 요청을 위임함.
```

#### 4-1. 위에 부분이 너무 이해가 안되서 찾아봤을떄는 이렇게 말해주었다...
요약
- 핸들러 어댑터는 ArgumentResolver를 통해 컨트롤러 메서드에 전달할 인자들을 결정하고, 메서드를 호출하여 컨트롤러가 요청 처리하도록함
- 그리고 ReturnValueHandler를 통해 컨트롤러의 처리 결과를 클라이언트에게 응답으로 보내기 위한 형태로 변환한다.
- 이렇게 핸들러 어댑터는 전/후처리 과정을 통해 요청과 으답의 처리를 관리하여 원활한 웹 애플리케이션의 동작을 지원한다.
```
ArgumentResolver
핸들러 어댑터가 컨트롤러 메서드를 호출할 때, 해당 메서드의 파라미터들에 전달할 값을 결정하는 역할을 한다.
예를 들어 @RequestParam 어노테이션을 사용하여 요청의 쿼리 파라미터 값을 메서드 파라미터에 바인딩하거나,
@RequestBody 어노테이션을 사용하여 요청 본문의 데이터를 자바 객체로 변환하여 메서드 파라미터에 전달하는 등의 작업을 수행한다.

ReturnValueHandler
컨트롤러의 메서드가 실행된 후, 반환된 결과를 적절한 형태로 변환하여 클라이언트에게 응답으로 보내기 위한 처리를 담당한다.
예를 들어, 컨트롤러의 메서드가 ResponseEntity를 반환하는 경우, ResponseEntity의 Body를 JSON으로 직렬화하여 클라이언트에게
응답으로 전달하는 작업을 수행한다.

리플렉션(Reflection)
ArgumentResolver가 요청에서 추출한 파라미터를 컨트롤러의 메서드에 전달할 때, 리플렉션을 사용하여 메서드를 호출한다.
리플렉션은 실행 시점에 클래스의 정보를 조사하고, 메서드를 호출하거나 필드에 접근하는 등의 작업을 수행할 수 있는 기능을 제공한다.
```

### 5. 비즈니스 로직을 처리함
```
이후에 컨트롤러는 서비스를 호출하고 우리가 작성한 비즈니스 로직들이 진행된다.
```

### 6. 컨트롤러가 반환값을 반환
- [ResponseEntity](https://lynmp.com)
```
비즈니스 로직 처리된 후에는 컨트롤러가 반환값을 반환함.
응답 데이터를 사용하는 경우에는 주로 ResponseEntity를 반환하게 되고, 응답 페이지를 보여주는 경우라면
String으로 View의 이름을 반환할 수도 있다.
요즘 프론트엔드와 백엔드를 분리하고, MSA로 가고 있는 시대에서는 주로 ResponseEntity를 반환한다.
```

### 7. 핸들러 어댑터가 반환값을 처리함
```
HandlerAdapter는 컨트롤러로부터 받은 응답 처리기인 ReturnValueHandler가 후처리한 후에 디스패처 서블릿으로 돌려준다.
만약 컨트롤러가 ResponseEntity를 반환하면,

HttpEntityMethodProcessor가 MessageConverter를 사용해 응답 객체를 직렬화하고 응답 상태(HttpStatus)를 설정한다.

만약 컨트롤러가 View 이름을 반환하면 ViewResolver를 통해 View를 반환한다.
```

### 8. 서버의 응답을 클라이언트로 반환함
```
디스패처 서블릿을 통해 반환되는 응답은 다시 필터들을 거쳐 클라이언트에게 반환된다. 이떄 응답이 데이터라면
그대로 반환되지만, 응답이 화면이라면 View의 이름에 맞는 View를 찾아서 반환해주는 ViewResolver가 적절한 화면을 내려준다.
```
