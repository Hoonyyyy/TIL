## HTML5
- 웹 문서 작성을 위한 HTML 태그 셋, 웹 애플리케이션 작성을 위한 API
- 웹 폼, 오디오, 캔버스, svg, 웹 스토리지, 웹 SQL 데이터베이스, 파일 입출력, 앱 워커, 위치정보 


```
<!-- 
	HTML기본문법
		. 대소문자를 구분하지않는다. > HTML, Html, html
		. 인용부호도 상관없다.	   > "웹문서", '웹문서', 웹문서
		. 문자열에 공란이 포함되어 있다면 반드시 인용부호를 써줘야 한다.
			"웹 문서" 
			
		. 시작태그와 종료태그로 구성된다.
			<시작>	</종료>
			<태그>	
			<태그/>
			
		. 속성
			<시작 속성명=속성값 속석명 = 속성값 > </종료>
		. 내용
		 	<시작> 내용(content, innerHTML) </종료>
		 	
	태그 와 요소(Element)
		. 태그 : 태그명
		. 요소 : <시작> 내용 </종료>
		
	태그의 대분류
		. 블록(block)태그
			- p, h1, div, ul 등
			- 항상 새로운 라인에서 시작한다 - 한줄을 차지한다
			- 줄바꿈이 되는것이다. br이 불필요
			- 너비와 높이 설정할 수 있다.
			
		. 인라인(inline)태그	
			- span, em, img, a, strong...등
			- 라인속의 한 부분을 차지한다. 
			- 줄바꿈 안됨. br이 필요
			- 너비와 높이 설정이 불가능하다.
			
		. Meta태그
			; head에 작성하는 태그
			- meta태그
				. name = ""  content = ""
				> charset = "utf-8"
				> name = "author"	content="홍길동"
				> name = "description"	content="설명내용"
				> name = "keywords" content="자장면,오뎅,,,"
			
			- base태그
				; 페이지에서 사용할 url의 중복을 피하기 위해 공통된 앞까지 설정
				<base href="http://www/mysite.com/score">
				<a href="math.html">
			
			- link태그
				; 외부파일을 이 문서로 가져와서 사용할때
				
			- title태그
				; 문서의 제목 / 태그 위에 마우스가 올라갔을때 팁을 주는 문구출력
				
			- style태그 :	꾸밈
				; css를 지정하기 위한 태그
				
			- scrpit태그 : 기능
				; javascript를 지정하기 위한 태그
 -->
```


### html 시인글 (줄바꿈 연습)
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body leftmargin="50" align="center">
			<h1>행	복</h1>
						<h3 align="right">한용운</h3>
	<hr>
	<div  width="400" height="600">				
	나는 당신을 사랑하고 당신의 행복을 사랑합니다.<br>
	나는 온 세상 사람들이 당신을 사랑하고<br>
	당신의 행복을 사랑하기를 바랍니다.<br><br>
	
	그러나 정말로 당신을 사랑하는 사람이 있다면<br>
	나는 그 사람을 미워하겠습니다.<br>
	
	그 사람을 미워하는 것은 당신을 사랑하는 마음의 한 부분입니다.<br>
	그러므로 그 사람을 미워하는 고통도 나에게는 행복입니다.<br><br>
	
	만일 온 세상 사람이 당신을 미워한다면<br>
	나는 그 사람을 얼마나 미워하겠습니까?<br><br>
	
	만일 온 세상 사람이 당신을 사랑하지 않고<br>
	미워하지도 않는다면<br>
	그것은 나의 일생에 견딜 수 없는 불행입니다.<br><br>
	
	만일 온 세상 사람이 당신을 사랑하고자 하여<br>
	나를 미워한다면 나의 행복은 더 클 수가 업습니다.<br><br>
	
	그것은 모든 사람이 나를 미워하는 원한의 두만강이 깊을수록<br>
	나의 당신을 사랑하는 행복의 백두산이 높아지는 까닭입니다.<br>
	</div>
		
</body>
</html>
```
### href="경로지정"
```html
	1) 절대경로
		; http://로 시작되는 웹사이트의 주소(url)를 사용해서 파일장소를 지정하는 방식
		; hhtp://localhos:8080/프로젝트명/패키지명/파일명.hrml

			루트계층		제1계층		제2계층 		제3계층
			-----------------------------------------
			index.html
			aaa ------- A.html
					|
					--- A2.html
					|
					bbb ------ B.html
							|
							---ccc ----- C.html

			ddd --- D.html


	2) 상대경로
		; 현재 파일로 부터 목적파일까지 상대적인 위치관계를 지정하는 방식

 -->
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<h3>절대경로로 파일을 호출합니다.</h3>
	<hr><br><br>

	<ul>
		<li><a href="http://localhost:8080/Ch02/path_절대경로/aaa/A.html"> A파일</a></li>
		<li><a href="http://localhost:8080/Ch02/path_절대경로/aaa/bbb/B.html"> B파일</a></li>
		<li><a href="http://localhost:8080/Ch02/path_절대경로/aaa/bbb/ccc/C.html"> C파일</a></li>
		<br>
		<br>
		<li><a href="http://localhost:8080/Ch02/path_절대경로/aaa/A2.html"> A2파일</a></li>
	</ul>

</body>
</html>		
		
		
		
```

상하,동일 객체 이동 html
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<h1>C파일입니다</h1>

	<h3>페이지 이동</h3>
	<ul>
		<li><a href="../../A.html">A로 이동</a></li>
		<li><a href="../B.html">B로 이동</a></li>
	</ul>
</body>
</html>
```
