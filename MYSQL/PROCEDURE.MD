## PROCEDURE.MD

CREATE PROCEDURE 프로시정 ( IN | OUT | INOUT 매개변수 데이터타입 [DEFAULT],, )
```
BEGIN
  지역변수선언 / 초기화
  SQL 문장...................;
  IF 조건식 then SQL문 [ELSE 조건식 THEN SQL문] [ELSE SQL문] END IF;
  CASE 받은변수 WHEN 비교변수 THEN SQL문 [WHEN 비교변수 THEN SQL문] [ELSE~] END CASE;
  CASE WHEN 조건식 THEN SQL문 ,,, [ELSE SQL문]
  WHILE 조건식 DO SQL문 END WHILE;
  REPEAT SQL문 UNTIL 조건식 END REPEAT;
  Loop이름 : LOOP ~~~ END LOOP;
  [다른 프로시저 호출가능]
END
```

CALL 프로시저명 (매개변수, 매개변수,,,@사용자매개변수)



## procedure 
```mysql
# 요청받은 강의코드의 이수과목이 전공필수이면 10%상향, 전공선택이면 5%상향, 교양필수이면 1%상향
# 하여 인원제한수를 재조정하는 '인원제한조정' 프로시저를 작성하시오 (단 소수점없이 반올림)

DELIMITER $$
CREATE PROCEDURE 인원제한조정(IN code VARCHAR(10))
BEGIN
    DECLARE required_credit VARCHAR(10);
    DECLARE current_limit INT;
    DECLARE new_limit INT;
    
    -- 요청받은 강의코드의 이수과목을 가져옵니다.
    SELECT 이수과목 INTO required_credit
    FROM 강의
    WHERE 강의번호 = code;
    
    -- 현재 인원제한수를 가져옵니다.
    SELECT 인원제한 INTO current_limit
    FROM 강의
    WHERE 강의번호 = code;
    
    -- 이수과목에 따라서 인원제한수를 조정합니다.
    IF required_credit = '전공필수' THEN
        SET new_limit = ROUND(current_limit * 1.1);
    ELSEIF required_credit = '전공선택' THEN
        SET new_limit = ROUND(current_limit * 1.05);
    ELSEIF required_credit = '교양필수' THEN
        SET new_limit = ROUND(current_limit * 1.01);
    ELSE
        -- 유효하지 않은 이수과목이면 인원제한수를 그대로 유지합니다.
        SET new_limit = current_limit;
    END IF;
    
    -- 새로운 인원제한수를 업데이트합니다.
    UPDATE 강의
    SET 인원제한 = new_limit
    WHERE 강의번호 = code;
END$$
DELIMITER ;

call 인원제한조정('c021');

SELECT 인원제한
FROM 강의
WHERE 강의번호 = 'c021';

SELECT *
FROM 강의;
```
