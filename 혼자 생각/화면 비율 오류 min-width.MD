# min-width 값 넣으면 전체 페이지에 이미지 넣었던거 오류를 잡을 수 있다

- 2일 동안 못고쳤던거 드디어 고쳤다..
- 여러가지 찾느라 다른 지식이 많이 쌓였다.. maring flex z-index 등등등...

### 예시코드
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Full Screen Div</title>
    <link rel="stylesheet" href="normalize.css">
    <style>

        #container1 {
            width: 100vw;
            height: 300px;
            min-width: 1000px;
            background-image: url("./image/cat5.jpg");
            background-size: cover;

        }

        #container1>#c {
            width: 1000px;
            height: 100px;
            background-color: antiquewhite;
            margin: 0 auto;
            display: flex;
        }


        
        /* 높이가 300px인 div */
        #container2 {
            width: 1000px;
            height: 300px;
            background-color: lightcoral;
            margin: 0 auto;
        }

        #a{
            width: 1000px;
            height: 200px;
            background-color: aqua;

        }
    </style>
</head>
<body>
    <div id="container1">
        <div id="c">
            <div>a</div>
            <div>b</div>
            <div>c</div>
            <div>d</div>
        </div>
    </div>

    <div id="container2">
        <div id="a">a</div>
    </div>
</body>
</html>

~~~
