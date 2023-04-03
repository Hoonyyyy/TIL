## fixed를 이용해서 위치잡는게 더욱 좋다.
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<style>
	body {
		position: relative;
	}

	#ul1 {
		position: fixed;
		left: -35px;
		bottom: -15px;
		list-style: none;
		margin-bottom: 20px;
	}

	#ul1>li {
		display: inline-block;
		background: gray;
		color: white;
		text-align: center;
		width: 150px;
		height: 30px;
	}

	#ul2 {
		list-style: none;
		position: fixed;
		right: 0px;

	}

	#ul2>li {
		background: lightgray;
		margin-bottom: 5px;
		width: 100px;
		height: 25px;
	}


</style>
<body>

	<ul id="ul1">
		<li>하단메뉴1</li>
		<li>하단메뉴2</li>
		<li>하단메뉴3</li>
	</ul>


	<ul id="ul2">
		<li>고정메뉴1</li>
		<li>고정메뉴2</li>
		<li>고정메뉴3</li>
		<li>고정메뉴4</li>
	</ul>


</body>
</html>
```
