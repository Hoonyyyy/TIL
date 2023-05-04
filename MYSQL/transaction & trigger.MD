## 트랜잭션 및 트리거.MD


### 트리거란?
```
  어떤 테이블의 데이터가 변경될 때 자동으로 지정된 애플리케이션이 동작되거나
  다른 테이블의 데이터를 변경하도록 설계된 *저장프로시저*의 특별한 형태이다. 
  테이블에서 수정, 삭제, 삽입이 발생하면 트리거가 자동호출되어 전체적인 데이터베이스의 구조를 바로 잡는 역할을 한다.
  매개변수를 사용할 수 없다.
```

#### 트리거 활용
```
  데이터베이스의 무결성을 위해 테이블 정의시 제약조건을 명시하는 방법을 사용한다.
  복잡한 데이터의 적합성 검사에 활용
  >> 광범위한 참조 무결성 검사에 활용다.
```

#### 트리거 단점
```
  연속적인 트리거 실행은 시스템 성능을 떨어트린다.
  무한루프 주의!
```

#### 트리거 종류 및 구현
```
		종류
			      - 입력할때...		before insert, after insert
          	- 수정할때...		before update, after update
          	- 삭제할때...		before delete, after delete
            
		구현
			CREATE TRIGGER 트리거명 발생시점 이벤트종류
			  ON 테이블
       for each row	// 각각의 행(레코드)에 대해서
       begin
				SQL문		// old.컬럼, new.컬럼
			 end
                    
			* old : 변경이 가해지기 전 레코드 - old테이블
			  new : 변경이 가해진 후 레코드 - new테이블
                    
      - INSERT	new
      - UPDATE	old, new
      - DELETE	old
```



### 트랜잭션(Transaction)
- Transaction should be must all performed or nothing performed!!
```
  DBMS에서 다루는 논리적인 작업의 단위
  서로 연관된 하나 이상의 명령들로 이루어진 논리적인 작업단위
```

#### 트랜잭션이 필요한 이유?
```
  장애발생 시 복구작업의 단위가 된다.
  연관된 여러 작업이 동시에 같은 데이터를 다룰때 작업의 단위를 분리하는 단위가 
  				홍길동이가 조회를 해서 5000원이 있는지 확인한다 --> 실행
                		5000원을 출금한다. ( - )		------> 오류!!!
               			동생에게 이체한다 ( + )		      ------> 실행
                		잔액을 조회한다.			------> 실행
				
				반영(commit)
      	>> 업무의 논리적인 작업단위를 정의한 것이다.
				
	. commit - 1) 자동 커밋 : insert문, update문, delete문 자동으로 커밋되는 트랜잭션이다.
			 - set autocommit = 0; (비활성화)
       - set autocommit = 1; (활성화)
			 
		   2) 명시적으로 커밋 - 트랜잭션
			 - 시작시점, 커밋, 롤백하는 시점을 직접 명시해야 한다.
    


	-- SIGNAL SQLSTATE '45000' 문
	--  사용자가 오류를 강제로 발생시키는 함수
	--  사용자가 정의한 오류 메시지를 출력
	--  사용자가 시도한 INSERT는 롤백처리한다.



```

### 트리거 및 트랜잭션 예제
```mysql
# update 트리거생성
delimiter $$
create trigger before_예금통장_update before update
	on 예금통장
    for each row
    begin
		declare message_text varchar(45);
		if new.잔액 < 0 then
			signal sqlstate '45000'
				set message_text = '잔액이 부족합니다';
		end if;
    end $$
delimiter ;

# 트랜젝션을 프로시저로 만들어서 송금처리 작업단위를 처리한다.

delimiter $$
CREATE procedure 송금 (in 이체금액 int)
BEGIN
	
    declare exit handler for sqlexception rollback;
		-- exit handler : 특정이벤트 (sqlexception)발생시 특정작업(rollback)을 수행해라.
        
	start transaction;
		update testdb.예금통장
        set 잔액 = 잔액-이체금액
        where 예금주아이디 = "001";
        
        update testdb.예금통장
        set 잔액 = 잔액+이체금액
        where 예금주아이디 = "002";
    commit;
END $$
delimiter ;

select *
from 예금통장;

call 송금(2000);
```
