# URI, URL, URN

## URI (Uniform Resource identifier)
- 리소스를 구분할 수 있는 식별자이다.
```
https://main.com/93

URI 통신 방식 : https
도메인 : main.com
리소스 디렉토리 93번

웹 브라우저에 URI 전송하면 main.com 도메인이 가르키는 IP Address의 93번 글에 접근하게 된다.
```

## URL (Uniform Resource Locator)
- 리소스의 경로(Location)을 기반으로 식별
- 4가지 요소 Protocol, HostName, Port, Path or Query
```
https://main.com:443/93

https : Protocol
main.com : HostName (IP Address)
443 : Port
93 : Path or query
```

#### Port란?
- 컴퓨터가 각종 신호, 정보 등을 주고 받을 수 있도록 해주는 통신 통로
- 컴퓨터 안에서 프로그램을 찾기 위한 수단, 즉 각 프로세스가 위치한 방 번호
```
예시 
어떤 사람이 보낸 물건이 집에 도착함.
이떄 보낸 사람은 우리집 주소(=IP 주소)를 알아서 보낼 수 있다.
집에 도착은 했지만 정확히 누구에게 온 물건인지는 모름
나한테 온 물건이라면 내가 있는 방에 전달해야 함 이떄 '포트'가 이 정보를 알려줌
```


## URN 


## URN
- 리소스의 이름(Name)을 기반으로 식별하는것
- 얘는 실제도 사용되는 경우가 없어 대부분 URI는 URL과 같다고 봐도 무방하다.
