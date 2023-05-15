# forward redirect 차이

```
Forward와 Redirect 차이
    1)  Forward
        . URL이 변경되지 않는다.
        . request, response가 유지된다.
        . request에 들어 있는 값이 유지된다.
        . 데이터설정과 유지를 위해서 setAttribute() getAttribute()를 활용한다
        . request.forward(location)
        
        정리
        . 서버 내부에서 직접 요청을 전달하는 방식으로, 요청과 응답 객체가 동일한 쓰레드에서 처리하기에
        . 요청 객체의 속성(Attribute)을 그대로 가져와서 사용할 수 있다.
        
    2)  Redirect
        . 웹서버가 웹브라우저에게 다른 페이지로 이동하라고 지시하는 것을 의미한다.
        . URL이 변경된다.
        . 요청시마다 request, response객체가 새로 생성된다.
        . getAttribute()를 사용할 수 없다.   getParameter()를 시용해야 한다.
        . 주소줄에 한글/특수문자가 존재한다면 반드시 URLEndcode를 해서 전송해야 한다.
        . response.sendRedirect()
        
        정리
        . 서버에서 새로운 요청을 생성하여 브라우저에게 보내는 방식으로, 요청과 응답 객체가 서로 다른
        . 쓰레드에서 처리됨. 새로운 요청이 생성되기에 요청 객체의 속성은 초기화된다 그렇기에
        . getAttribute() 메서드로 요청 객체의 속성을 가져올 수 없다
        . 따라서 속성 값을 새로운 요청에 전달하기 위해 쿼리 파라미터나 세션등을 사용해야 한다.
        . 쿼리 파라미터를 사용하면 URL 뒤에 속성 값이 추가되어 전달되며, 세션을 사용하면 새로운 요청에
        . 서도 속성 값을 유지할 수 있다
```
