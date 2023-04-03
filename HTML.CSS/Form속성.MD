```
	웹 폼
		; 웹 페이지를 통해서 사용자 입력을 받는 웹폼(또는 폼)이라 한다.

		- form태그 속성
			.action: 입력받은 데이터를 어디로 보낼것이냐?
	 					받은 데이터를 처리할 서버응용프로그램 경로

			. method: 폼 데이터를 웹서버에 전송하는 방식
			. target: 웹 서버 응용프로그램으로 부터 전송받은 데이터를
						출력할 윈도우 이름
			. enctype: 폼 데이터를 웹 서버로 전송할 때 암호화 방식 지정 

		- 폼의 종류
			. button : 전송, 이벤트처리의 버튼 용으로 사용... 
					        버튼을 사용할때는 타입을 버튼으로 명시
			. radiobox :  
			. checkbox
			. input
				- text: 한줄 텍스트 입력창
				- password: 암호 입력을 위한 한줄 텍스트 입력창
	      		- image: 이미지 버튼
				- button: 버튼
				- checkbox: 체크박스
				- radio: 라디오버튼
				- month | week | date | time | datetime | datetime-local
				- number | range : 스핀버튼과 슬라이드바로 편리한 숫자입력창
				- color : 색 입력을 쉽게 하는 컬러 다이얼로그
				- email | url | tel | search : 형식검사기능
				- file: 로컬 컴퓨터의 파일을 선택하는폼요소


```

### 로그인 or 휴대전화 번호 치면서 form 연습
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<form>
		아 이 디: <input type="text" name="login" value="" size="12"><br>
		암  &nbsp;호: <input type="password" name="pwd" value="" size="12"><br>
		휴대번호: <input type="text" name="phon1" size="3" maxlength="3">-
				<input type="text" name="phone2" size="4" maxlength="4">-
				<input type="text" name="phon3" size="4" maxlength="4">

		<input type="submit" value="등록">&nbsp;
		<input type="reset" value="취소">

	</form>
</body>
</html>
```

### form - search연습
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>

		<form action="#" name="Log_fo" method="get" target="" enctype="">
<!-- 			<input type=""> -->
			사용자 ID: <input type="text" value="" size="15"><br>
			비밀번호&nbsp;: <input type="password" value="" size="15"><br> 

			<input type="submit" value="전송"> &nbsp;
			<input type="reset" value="취소">
		</form>
		<hr>
			
		<form name="search_fo"
			  action="https://search.naver.com/search.naver/"
			  method="get"
 			  list="중국음식">


			검색단어: <input type="text" list="중국음식" name="query"><br><br>
	<!-- 		<datalistid id="중국음식">
				<option>짜장면</option>
				<option>짬 뽕</option>
				<option>탕수육</option>
			</datalistid> -->
			검색하기: <input type="submit" value="검색">

		</form>

</body>
</html>
```
