### utf-8 설정은 다른처리보다 앞에서 해줘야한다.


```java
protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		
		request.setCharacterEncoding("utf-8");
		
		process(request, response);
		
		
	}
```
