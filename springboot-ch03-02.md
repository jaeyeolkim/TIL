### 스프링부트 기능소개#2

3.2 외부구성
* 동일한 애플리케이션을 각기 다른 환경에서 실행할 수 있도록 외부에서 조작할 수 있다.
* YAML 파일(.yml), properties 파일(.properties), 환경변수 그리고 커맨드라인 실행인자를 이용할 수 있다.
* 이 속성값은 @Value 애노테이션을 통해서 스프링 빈에 주입하거나 Environment를 이용해서 접근하거나 @ConfigurationProperties를 통해 연결할 수도 있다.

* SpringApplication은 다음 위치에 있는 application.yml(또는 .properties)파일을 읽어서 Environment에 속성을 적재한다.
  1. 현재 디렉토리 하위에 있는 /config
  2. 현재 디렉토리
  3. 클래스패스 /config 패키지
  4. 최상위 클래스패스
  
* properties를 대신하여 YAML 사용하기
  * YAML은 JSON의 확장판이라고 할 수 있다.
  * 계층적으로 구성된 데이터를 사람이 쉽게 읽을 수 있는 형식으로 표현한다.
  * 클래스패스 상에 SnakeYAML을 가지고 있다면 자동으로 properties를 대신하여 YAML을 지원할 수 있다.
  * YAML 문서에서 **spring.profiles** 키를 이용해서 다중 프로파일을 다룰 수 있다.
  ~~~
  #default
  logging:
    level:
    com.kjy: DEBUG
  server:
    port: 9000
  ---
  #local
  spring:
    profiles: local
  logging:
    level:
    com.kjy: TRACE
  server:
    port: 9000
  ~~~
