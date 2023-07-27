# Application, Session, Request, Page

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99E89A3C5C6D04451B">

## Page
페이지 내에서 지역변수처럼 사용

#### Page Scope
- PageContext 추상 클래스를 사용
- JSP 페이지에서 pageContext라는 내장 객체로 사용 가능
- forward가 될 경우 해당 Page scope에 지정된 변수는 사용할 수 없다.
- 사용방법은 Application scope나 Session scope, request scope와 같다.(setAttribute, getAttribute)
- 마치 지역변수처럼 사용된다는 것은 다른 Scope들과 다르다.(해당 jsp나 서블릿을 사용할 때만 사용)
- jsp에서 pageScope에 값을 저장한 후 해당 값을 EL표기법, JSTL에서 사용할 때 사용된다.

## Request
http요청을 WAS가 받아서 웹 브라우저에게 응답할 때까지 변수가 유지되는 경우 사용

#### Request Scope
- http 요청을 WAS(서버)가 받아서 웹 브라우저에게 응답할 때(response)까지 변수값을 유지하고자 할 경우 사용한다.
- HttpServletRequest 객체를 사용한다.
- JSP에서는 request 내장 객체를 사용한다.
- 서블릿에서는 HttpServletRequest 객체를 사용한다.
- 값 저장 setAttribute(), 값 읽기 getAttribute()
- forward시 값을 유지하고자 사용함

## Session
웹 브라우저 별로 변수가 관리되는 경우 사용(생성되고, 지워지기 전까지)

#### Session Scope
- 웹 브라우저(클라이언트)별로 변수를 관리하고자 할 경우 사용한다.(session 지속시간만료, 브라우저 종료시 사라짐)
- 웹 브라우저간의 탭 간에는 세션정보가 공유되기 때문에, 각각의 탭에서는 같은 세션정보를 사용할 수 있다.
- HttpSession 인터페이스를 구현한 객체를 사용한다.
- JSP에서는 session 내장 객체를 사용한다.
- 서블릿에서는 httpServletRequest의 getSession()메서드를 이용하여 session 객체를 얻음 (request.getSession())
- 값 저장시 setAttribute(), 값 읽기 getAttribute()
- 로그인 처럼 사용자별로 유지가 되어야 할 정보가 있을 때 사용함

## Application
웹 어플리케이션이 시작되고 종료될 때까지 변수가 유지되는 경우 사용

#### Application Scope
- 웹 어플리케이션이 시작되고 종료될 때까지 변수를 사용할 수 있다.
- ServletContext 인터페이스를 구현한 객체를 사용한다.
- jsp에서는 application 내장 객체를 이용한다.
- 서블릿의 경우는 getServletContext()메서드를 이용하여 application객체를 이용한다.
- 웹 어플리케이션 하나당 하나의 application객체가 사용됨 (프로그램 실행되는동안 계속 객체 유지)
- 값을 저장할 때는 setAttribute(), 값 읽을때는 getAttribute()
- 모든 클라이언트가 공통으로 사용해야 할 값들이 있을 때 사용함 (바뀌어도 누적됨)
- intelliJ에서 하나의 Project가 하나의 Application이라고 생각하



https://zester7.tistory.com/46
https://starkying.tistory.com/entry/Servlet-JSP%EC%9D%98-4%EA%B0%80%EC%A7%80-Scope
