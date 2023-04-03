## iframe
```

<!-- 
	iframe
		- 윈도우 또는 간단한 윈도우라고 한다.

		<iframe src="URL"
				srcdoc="HTML문서텍스트"
				name = "프레임이름"	(target)
				width = ""		(디폴트 300)
				height = "" 	(디폴트 300)
				marginwidth = "" (윈도우창의 너비여백지정)
				marginheight = "" (윈도우창의 높이여백지정)

		<iframe태그를 지원하지 않는 브라우저입니다.
		</iframe>
		
		. iframe태그는 body에서만 사용해야한다.
		. src속성이 생략되면 iframe영역은 만들어지지만 빈 상태가 존재된다
		. 프레임에 출력할 HTML을 srcdoc로 직접 작성할 수 있지만,
		  src가 존재한다면 srcdoc는 무시된다.
		. 프레임안에 또 다른 프레임을 중첩시킬 수 있다.
		. inline-block 요소의 특징을 갖는다.



 -->


<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>

	<h3>인라인 프레임 구성</h3>
	<hr>

	<iframe src="F1_1프레임.html"
			width="49%"
			height="600"
			frameborder="0"
			marginwidth="150"
			marginheight="150"> 첫번째

	</iframe>
	<iframe
			src="F1_2프레임.html"
			width="49%"
			height="600"
	> 두번

	</iframe>


</body>
</html>
```

## target 값은 동일해도 된다.
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<h3 align="center">오늘의 메뉴</h3>
	<hr>

	<ul>
		<li>
			Coffee<br>
			&nbsp;- <a href="F1_coffee.html" target="coffee">아메리카노</a><br>
			&nbsp;- <a href="F1_coffee2.html" target="coffee">에스프레소</a><br>
			&nbsp;- <a href="f1_coffee3.html" target="coffee">라떼</a><br>
		</li>
	</ul>
	<hr>
	<ul>
		<li>
			Bread<br>
			&nbsp;- <a href="F1_bread.html" target="bread">바게뜨빵</a><br>
			&nbsp;- <a href="F1_bread2.html" target="bread">크루아상</a><br>
			&nbsp;- <a href="F1_bread3.html" target="bread">호밀빵</a><br>
		</li>
	</ul>
	<hr>
	<ul>
		<li>
			Drink<br>
			&nbsp;- <a href="F1_Drink.html" target="drink">레몬차</a><br>
			&nbsp;- <a href="F1_Drink2.html" target="drink">캐모마일</a><br>
			&nbsp;- <a href="F1_Drink3.html" target="drink">녹차</a><br>
		</li>
	</ul>

</body>
</html>
```
