## mybatis 사용시 발생 가능한 오류 대응
ibatis 에서 변환 작업 하면서 내용을 정리한다.
<br/>
<br/>
> ### java.lang.NumberFormatException 오류 처리
OGNL 표현식은 'Y' 를 char 로 변환해서 코드 값을 가져가기 때문에
java.lang.NumberFormatException: For input string: “Y” 와 같은 오류가 발생한다.
('YY' 와 같이 두 글자는 이상없지만 쌍따옴표로 통일하는 것이 좋겠다)
```
<if test='FLAG != "Y"'>
</if>
```
<br/>

> ### <code>\<if test='START_DATE != null and START_DATE != ""'></code> 의 의미
참고로 변환기(https://github.com/mybatis/ibatis2mybatis) 사용시 ibatis 의 isNotEmpty 태그가 위와 같이 변환된다.

* empty 이면 <code>\<if test='START_DATE != ""'></code> 조건에 걸린다.
```
paramMap.put("START_DATE", "");
<if test='START_DATE != ""'>
</if>
```

* 속성이 존재하지 않으면 <code>\<if test='START_DATE != null'></code> 조건에 걸린다.
```
paramMap.remove("START_DATE");
<if test='START_DATE != null'>
</if>
```
<br/>

> ### foreach 
```
<foreach collection="APPROVAL_STATUS" item="item" separator="," close=")" open=" IN (">
    #{APPROVAL_item} => 변환기
</foreach>
```
변환기는 위와 같이 된다. 아래와 같이 수정해야 원하는 결과를 얻게 된다.
```
<foreach collection="APPROVAL_STATUS" item="item" separator="," close=")" open=" IN (">
    '${item}'
</foreach>
```
<br/>

> ### selectKey 에는 order="BEFORE" 선언하여 selectKey 가 먼저 실행되도록 하자
미선언시 insert 후에 selectKey가 생성된다.
```
<selectKey ... order="BEFORE">
```
<br/>

> ### resultMap 선언시 jdbcType 변경
```
<result ... jdbcType="NUMBER" /> -> <result ... jdbcType="NUMERIC" /> 
<result ... jdbcType="VARCHAR2" /> -> <result ... jdbcType="VARCHAR" /> 
```
