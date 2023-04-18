## 특정한것에만 적용되게 하는것 event.target
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<script>

	

	function doing(event){
		let clickedElement = event.target;
		clickedElement.classList.toggle("enLarge");
	}

</script>
<style>


	div {
		text-align: center;
	}

	.enLarge {
		transform: scale(2.5);
	}

</style>
</head>
<body>
	<h3>아이템을 클릭하면 2.5배 크기로</h3>
	<hr>
	<h3>여름 방학 때 하고 싶은 거슬</h3>
	<div>
		<p onclick="doing(event)">. 자전거로 대한민국 일주</p>
		<p onclick="doing(event)">. 책 100권 읽기</p>
		<p onclick="doing(event)">. 철인 3종 경기 준비</p>
		<p onclick="doing(event)">. 자바스크립트 정복</p>
	</div>

</body>
</html>
```
