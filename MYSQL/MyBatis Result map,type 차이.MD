# MyBatis Result map,type 차이

https://pulpul8282.tistory.com/194


- 간단하게 정리할 수 있다.
```
resultType 은 반환타입으로 클래스 자체를 가져와 참조

resultMap은 반환타입으로 개발자가 xml 내에서 임의로 정의한 형식으로 참조(db컬럼명을 선언후 나는 자바에서 내가 원하는 명으로 뽑고싶다)
```


- 코드

```xml
<mapper namespace="FestivalDAO">
			<!-- vo                db table -->
	<resultMap type="festival" id="festivalResult">
		<id property="festival_name" column="FESTIVAL_NAME"/>
		<result property="festival_startdate" column="FESTIVAL_STARTDATE"/>
		<result property="festival_enddate" column="FESTIVAL_ENDDATE"/>
		<result property="festival_address" column="FESTIVAL_ADDRESS"/>
		<result property="festival_detail_information" column="FESTIVAL_DETAIL_INFORMATION"/>
		<result property="festival_showaddress" column="FESTIVAL_SHOWADDRESS"/>
		<result property="festival_number" column="FESTIVAL_NUMBER"/>
		<result property="festival_latitude" column="FESTIVAL_LATITUDE"/>
		<result property="festival_longitude" column="FESTIVAL_LONGITUDE"/>
		<result property="festival_fee" column="FESTIVAL_FEE"/>
		<result property="festival_instagram_name" column="FESTIVAL_INSTAGRAM_NAME"/>
		<result property="festival_instagram_address" column="FESTIVAL_INSTAGRAM_ADDRESS"/>
		<result property="festival_homepage_address" column="FESTIVAL_HOMEPAGE_ADDRESS"/>
		
		<result property="like_no" column="LIKE_NO"/>
		<result property="member_id" column="MEMBER_ID"/>
		
		<result property="festival_file_1" column="FESTIVAL_FILE_1"/>
		<result property="festival_file_2" column="FESTIVAL_FILE_2"/>
		<result property="festival_file_3" column="FESTIVAL_FILE_3"/>
		<result property="festival_file_4" column="FESTIVAL_FILE_4"/>
		<result property="festival_file_5" column="FESTIVAL_FILE_5"/>
		<result property="festival_file_6" column="FESTIVAL_FILE_6"/>
	</resultMap>


	<!-- 전체검색 -->
	<select id="getFestivalList_Month_All" resultMap="festivalResult">
		SELECT *
		FROM festival as f1
		join festival_address as f2
			on f1.festival_name = f2.festival_name
		WHERE MONTH(CURDATE()) BETWEEN MONTH(festival_startdate) AND MONTH(festival_enddate);
	</select>

	<!-- 상세검색 -->
	<select id="getFestival" resultType="festival">
		select *
			from festival as f1
			join festival_address as f2
				on f1.festival_name = f2.FESTIVAL_NAME
			join festival_insta as f3
				on f1.festival_name = f3.FESTIVAL_NAME
			join festival_fee as f4
				on f1.festival_name = f4.festival_name
			where f1.festival_name = #{festival_name}
	</select>

</mapper>
```
