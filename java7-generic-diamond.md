## java7 generic diamond

1. java SE 7 이전
```java
Map<String, List<String>> myMap = new HashMap<String, List<String>>();
```

2. java SE 7 부터는
```java
Map<String, List<String>> myMap = new HashMap<>();
```
* 컴파일러가 자료 타입을 유추할 수 있는 경우 다이아몬드를 선언할 수 있습니다.

3. 다이아몬드 생략시에는 unchecked conversion warning 이 발생합니다.
```java
Map<String, List<String>> myMap = new HashMap(); // unchecked conversion warning
```

* 참고
  * https://docs.oracle.com/javase/tutorial/java/generics/genTypeInference.html
