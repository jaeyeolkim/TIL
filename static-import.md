### java static import 사용하여 가독성을 높이자

* static 메소드 사용시 아래와 같이 일반적으로 사용한다.
```java
import StringUtil;

StringUtil.null2string(map.get("USER_CODE"));
StringUtil.null2string(map.get("USER_NAME"));
```

* static import 를 사용하면 코드를 줄이고 가독성을 높일 수 있다.
```java
import static StringUtil.null2string;
//또는 import static StringUtil.*;

null2string(map.get("USER_CODE"));
null2string(map.get("USER_NAME"));
```
  * 'StringUtil.' 쓰지 않아도 'null2string' 사용할 수 있다.

* import static StringUtil.*; 사용시에는 메소드의 출처를 알기 어려울 수도 있어서 협업시에는 좋지 않을 듯 하다.
* java 1.5 부터 사용 가능하다.
  * https://docs.oracle.com/javase/1.5.0/docs/guide/language/static-import.html
