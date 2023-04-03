## background
```
	.background-color	: 이미지가 없을경우는 배경색상이 나타난다.
	.background-image	: url() - 배경이미지
	.background-repeat	: repeat-x, repeat-y 이미지 반복여부
	.background-attachment	: 이미지 스크롤 여부
	.background-position : x  y - 이미지위치정
	.background-size : contain, cover, auto 배경(부모)크기에 일정크기로 배치시킴
			- contain : 너비와 높이의 비율을 유지한채, 이미지가 전체 들어갈 수 있도록
			- cover : 너비와 높이의 비율을 유지한채, 해당 이미지 하나만으로 표시영역을 덮을 수 있는
			- auto : 너비와 높이의 비율을 유지한채, 이미지크기가 자동변경
				한개의 값만 지정하면 너비가 지정된 것으로 판단하고 높이는 auto가 된다.

	.background-clip : border-box, padding-box, content-box 배경을 표시할 범위 지정
```

## 그라데이션 표현
```
	원형 그라데이션
		. radial-gradient(모양 크기(반지름) at 시작)
		. 모양 : circle, ellipse
		. 크기 :
				closest-side :	circle  - 원의 중심점에서 가까운 박스의 변에 내접
								ellipse	- 타원의 중심에서 가까운 박스의 변에 내접
				farthest-sdie :	circle	- 원 가장 먼 변에 내접
								ellipse - 타원 가장 먼 변에 내접
				farthest-corner : 원 또는 타원의 중심에서 가장 먼 박스의 모서리에 내접
				closest-corner  : 가장 가까운 모서리에 내접
```
