## input에서 name과 id의 차이

```html
    <p>
			<label for="user_name1">이름</label>
			<input type="text" name="user_name" id="user">
		</p>
		<p>
			<label for="user_name2">이름</label>
			<input type="text" name="user_name" id="user">
		</p>
```

```
HTML에서 name과 id 속성은 각각 다른 용도를 가지고 있습니다.

name 속성은 폼 데이터를 서버로 전송할 때 해당 입력 요소의 이름을 지정합니다.
서버에서 이 이름을 사용하여 데이터를 처리합니다.

id 속성은 문서 내에서 해당 요소를 고유하게 식별하기 위한 식별자 역할을 합니다.
CSS나 JavaScript에서 해당 요소를  참조할 때 주로 사용합니다.
따라서 같은 이름(name)을 가진 여러 입력 요소들이 있을 때,
서버에서 구분하기 위해서는 각각 다른 id 값을 부여해야 합니다.

예를 들어, 로그인 폼에서 아이디 입력란과 비밀번호 입력란은 모두 name="user"로 설정되어 있지만,
각각 다른 id 값을 가지고 있습니다. 이렇게 하면 서버에서 전송된 데이터를 각각의 입력 요소로 구분할 수 있습니다.
```
