### 스프링부트 기능소개#2

3.2 외부구성
* 동일한 애플리케이션을 각기 다른 환경에서 실행할 수 있도록 외부에서 조작할 수 있다.
* YAML 파일(.yml), properties 파일(.properties), 환경변수 그리고 커맨드라인 실행인자를 이용할 수 있다.
* 이 속성값은 @Value 애노테이션을 통해서 스프링 빈에 주입하거나 Environment를 이용해서 접근하거나 @ConfigurationProperties를 통해 연결할 수도 있다.
