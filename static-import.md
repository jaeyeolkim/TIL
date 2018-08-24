### java static import 정리

* static 메소드 사용시 아래와 같이 사용해왔다.
```java
import com.util.StringUtil;

user.setUserCode(StringUtil.null2string(map.get("USER_CODE")));
user.setUserName(StringUtil.null2string(map.get("USER_NAME")));
user.setDeptCode(StringUtil.null2string(map.get("DEPT_CODE")));
user.setDeptName(StringUtil.null2string(map.get("DEPT_NAME")));
```

* static import 를 사용하면 <code>StringUtil.</code> 없이도 <code>null2string</code> 사용할 수 있다.
```java
import static com.util.StringUtil.null2string; //또는 import static com.util.StringUtil.*;

user.setUserCode(null2string(map.get("USER_CODE")));
user.setUserName(null2string(map.get("USER_NAME")));
user.setDeptCode(null2string(map.get("DEPT_CODE")));
user.setDeptName(null2string(map.get("DEPT_NAME")));
```

* import static com.util.StringUtil.<code>*</code>; 사용시에는 메소드의 출처를 알기 어려울 수도 있어서 협업시에는 좋지 않을 듯 하다.  
* java 1.5 부터 사용 가능하다.
  * https://docs.oracle.com/javase/1.5.0/docs/guide/language/static-import.html
