# Ajax

## Ajax ( Asynchronous JavaScript And XML )
- 서버와 비동기적으로 데이터 주고받는 자바스크립트 기술

### 사전 지식
- 서버
- 서버란 ?
- 유저가 데이터를 오규하면 데이터 보내주는 프로그램
- 이거주세요! 하면 주는것
- 원하는 데이터 URL이 뭔데?
- 그 URL로 GET요청해라
```

```

- 새로고침 없이 서버에게 GET요청하는 쪼그마한 JS코드

### 장점
- 웹페이지 전환이 부드러워짐


### 방법
- asnyc 방법 있음
```html
<script>
  fetch('https://codingapple1.github.io/price.json')
  .then(response) => {
    if (!response.ok) {
      throw new Error('400 아니면 500 에러남')
    }
    return response.json()
  })
  .then((결과) => {
    console.log(결과)
  })
  .catch(() => {
    console.log('에러남')
  })

</script>
```

### jQuery에 ajax 방법도 있음

