# 코드로 이해하기

jsonData객체
- JSON데이터를 표현하는 객체
- 객체 내부에는 다양한 데이터 타입과 구조를 가진 속성들이 포함되어 있다.

JSON.stringify()
- 자바스크립트 객체를 JSON형식의 문자열로 변환시켜줌

JSON.parse()
- JSON형식의 문자열을 자바스크립트 객체로 변환

jsonObject
- JSON데이터를 자바스크립트 객체로 변환한 결


```html
// JSON 데이터 생성
const jsonData = {
  "name": "John Doe",
  "age": 30,
  "isMarried": true,
  "hobbies": ["reading", "running", "swimming"],
  "address": {
    "city": "New York",
    "country": "USA"
  },
  "sayHello": function() {
    console.log("Hello!");
  }
};

// JSON 데이터를 문자열로 변환
const jsonString = JSON.stringify(jsonData);

// 문자열을 JSON 데이터로 변환
const jsonObject = JSON.parse(jsonString);

// JSON 데이터 접근
console.log(jsonObject.name); // John Doe
console.log(jsonObject.age); // 30
console.log(jsonObject.hobbies[0]); // reading
console.log(jsonObject.address.city); // New York

// 함수 호출
jsonObject.sayHello(); // Hello!
```


### JSON
```html
<!--
	JSON객체
		- 데이터를 저장하거나 전송할 때 많이 사용되는 경량의 Data 교환형식
		- 데이터 포맷이다.
		- 단순히 데이터를 표시하는 방법이다.
			. 서버와 클라이언트간의 데이터 전송시 많이 사용
			. 자바스크립트의 Object객체 표기법과 매우 유사하다.
			. JSON.stringify(객체명)
					- 자바스크립트의 객체를 JSON타입으로 전환
			. JSON.parse(JSON타입데이터)
				- JSON타입의 데이터를 자바스크립트의 객체로 전환
			. 프로그램의 언어와 상관없이 사용할 수 있는 데이터 교환형식이다.
			. 대부분 언어에서는 JSON데이터를 처리할 수 있는 라이브러리를 제공한다.

			클라이언트 <<<	JSON형식으로 데이터	>>> 서버
			(브라우저)

			. 표기법
				- 키와 값 쌍으로 표기한다.
				- 키는 반드시 쌍따옴표를 붙여서 작성해야 한다.
				- "키":"값", "키":"값",,,,,,

	리터럴 표기법
			. 중괄호를 이용해서 프로퍼티와 메서드를 한번에 작성할 수 있다.
			. 가독성이 높다.
			. 키를 " " 처리해도 되고 생략해도 된다.
			. 데이터에는 값이 문자일경우 "", 숫자는 생략, 객체, 배열도 가능하다.
			. 객체명.키로 호출하여 사용한다.
			. this를 붙이지 않는다.
			. 함수를 내부에서 정의할 수도 있고, 외부에서 정의(괄호는 생략)할 수도 있다.
			. 표기법
				- 키 : "값", 키:"값",,,,,
 -->
```


### 예시2 왔다갔다
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
<script>
	function Student(name,dept,grade){
		this.name = name;
		this.dept = dept;
		this.grade = grade;
		this.phone = "010-1111-2222";
		this.study = function() {
			document.write("<h3>열심히 공부합니다</h3>");
		}
	}

	let person = {
		name	: "홍길동",
		age		: 39,
		hobby	:['축구','야구','배구']	
	}

</script>
</head>
<body>
	<script>
		let s1 = new Student("홍길동","컴공",3);
		let s2 = new Student("강감찬","건축",2);
		
		// 클라이언트와 서버간 통신
		//	. 자바스크립트 객체(Object) >> JSON.stringify(객체) >> JSON(String)
		//	. JSON을 >> 객체로 활용할때... >> JSON.parse(JSON데이터) >> 활용

		document.write(typeof(s1)+"<br>");
		let s3 = JSON.stringify(s1);
		document.write(typeof(s3)+"<br>");
		document.write(s3+"<br>");

		let s4 = JSON.parse(s3);
		document.write(typeof(s4)+"<br>");

	</script>
</body>
</html>
```
