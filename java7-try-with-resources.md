## try with resources 

1. java SE 7 이전 
```java
static String readFirstLineFromFileWithFinallyBlock(String path)
                                                     throws IOException {
    BufferedReader br = new BufferedReader(new FileReader(path));
    try {
        return br.readLine();
    } finally {
        if (br != null) br.close();
    }
}
```

2. Java SE 7 부터는
```java
static String readFirstLineFromFile(String path) throws IOException {
    try (BufferedReader br = new BufferedReader(new FileReader(path))) {
        return br.readLine();
    }
}
```
* 자원 해제를 생략하고 JVM에 맡길 수 있다.
* try 안에 여러개를 넣고 싶을 때는 ';' 로 구분하여 사용 가능하다.
* 참고 자료
  * https://docs.oracle.com/javase/tutorial/essential/exceptions/tryResourceClose.html
