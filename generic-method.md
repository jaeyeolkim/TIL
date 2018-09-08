## generic method
제너릭 메소드는 매개 타입과 리턴 타입으로 타입 파라미터를 갖는 메소드를 말한다.
리턴 타입 앞에 <> 기호를 추가하고 타입 파라미터를 기술한 다음,
리턴 타입과 매개 타입으로 타입 파라미터를 사용하면 된다.

```java
pulbic <T> Box<T> boxing(T t){
}

public <타입 파라미터, ...> 리턴타입 메소드명(매개변수, ...){
}
```

```java
Box<Integer> box = boxing(1);
```
