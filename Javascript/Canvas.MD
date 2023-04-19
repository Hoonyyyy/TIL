# Canvas

### Canvas 원 닫을때 context.closePath()함해줘야함

```html
<!-- 
   	캔버스
    	. 자바스크립트 코드로 웹페이지에 자유롭게 그래픽을 수행할 수 있도록 해주는 DOM이다.
    	. 브라우저 화면에 공간을 캔버스에 할당하고 그래픽 기능을 이용해서 그린다.
    	. 캔버스의 그래픽은 자바스크립트 코드롬나 가능하다.
    	. 도형, 글자, 이미지(변환), 실시그래프, 애니메이션, 대화형게임
    	. 지도등을 플러그인없이 만들때 사용된다.

     	. 웹표준이다.
    	. 벡터방식(svg)이 아니라 비트맵 렌더링 방식으로 브라우저에 직접 그리므로 매우 빠르다.
      	. 2차원뿐만 아니라 3차원도 지원한다.
      	. 2차원('2d'), 3차원('webg1')도 지원한다.
      
	canvas태그 활용
		. id, style, width, height 속성을 적용한다.
		. getContext()	:	context 객체 반환

	context객체 : 그리기 도구
		
		- strokeStyle	:	선색
		- fillStyle		:	면의색
		- lineWidth		:	선의 두께
		- font			:	텍스트 폰트
		- textAlign		:	텍스트 정렬

		1) 경로 만들기
			- beginPath()	:	이전 경로를 모두 지우고 새로 시작
			- moveTo()		:	경로의 새로운 점을 만든다.
			- lineTo()		:	연결하는 선을 추가한다.
			- rect()		:	경로에 사각형을 추가한다.
			- arc()			:	경로에 원(원호)를 추가한다.
			
			- stroke()		:	경로에 담겨있는 모든 도형의 선을 그린다.
			- fill()		:	경로에 담겨있는 모든 도형의 면을 그린다.

		2) 직접 도형그리기
			- strokeText	:	문자열 그리기
			- strokeArc()
			- fillRect()
			- filArc()

			- drawImage()	:	이미지를 그린다
			- clearRect()	:	사각형을 지운다
			
			~~

 -->
 
 <!-- 
		. arc(x1, y1, 시작각, 회전각, 시계방향)
			* 360도 2𝝅
 -->
 
 <!-- 
	rect(x,y,w,h)	-	사각형 경로에 x,y,w,h 적용
	strokeRect(x,y,w,h)	-	캔버스에 직접그린다.	
 -->
 
```


### 예제
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<canvas
		id="myCanvas"
		style="background: lightblue;"
		width="1000"
		height="1000"
	></canvas>

	<script>
		let canvas = document.getElementById('myCanvas');
		let context = canvas.getContext('2d');


		context.fillStyle = "black";
		context.fillRect(100,100,150,150);
		context.stroke();
		
		context.fillStyle = "gray";
		context.fillRect(300,300,300,300);
		context.fillStyle = "red";
		context.fillRect(400,400,100,100);
		context.stroke();

		context.beginPath();
		context.lineWidth = '20'
		context.strokeStyle = 'green';
		context.arc(800,100, 50, Math.PI/1, true);
		context.stroke();

		// context.beginPath();
		// context.lineWidth = '20'
		// context.strokeStyle = 'red';
		// context.fillStyle = 'yellow';
		// context.arc(800,300, 50, Math.PI/3, false);
		// context.fill();
		// context.stroke();
		

		context.beginPath();
		context.strokeStyle = '#a91900ff';
		context.lineWidth=40;
		context.arc(800,500,150,0,(1.5*Math.PI),false);
		context.closePath();
		context.stroke();
		context.fillStyle='yellow';
		context.fill();
		

	</script>

</body>
</html>
```
