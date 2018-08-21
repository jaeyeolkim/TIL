## 스프링 부트 기능소개

* SpringApplication
  * SpringApplication 클래스는 스프링 애플리케이션 실행시 main() 메서드를 통해 여러 가지 편의를 제공한다.
  ```java
  public static void main(String[] args){
      SpringApplication.run(SpringBootApplication.class, args);
  }
  ```
  * 구동 실패시 **FailureAnalyzers** 를 통해 문제를 출력한다.
  * FailureAnalyzers 가 아니더라도 application.yml 에 <code>debug: true</code> 속성을 추가하면 자동구성 보고서를 통해 볼 수 있다.
  * 배너기능
    * 애플리케이션 구동시 출력되는 배너를 변경할 수 있다.(이미지도 가능)
  * SpringApplication 재정의
  ```java
  public static void main(String[] args){
      SpringApplication app = new SpringApplication(SpringBootApplication.class);
      app.addListeners(new ApplicationPidFileWriter());
      app.run(args);
  }
  ```
    * 또는 application.yml 에 설정할 수 있다.
  * SpringApplicationBuilder 는 parent와 child 메서드를 포함하고 있어 계층을 구성하거나 여러 메서드를 연이어 호출할 수 있다.
  ```java
  new SpringApplicationBuilder()
          .sources(Parent.class)
          .child(Application.class)
          .bannerMode(Banner.Mode.OFF)
          .run(args);
  ```
  * 애플리케이션 이벤트 및 리스너
  ```
  몇 가지 이벤트는 ApplicationContext가 생성되기 전에 발생하기 때문에 @Bean과 같은 컴포넌트를 리스너로 등록할 수 없다. 
  대신 SpringApplication.addListener(...) 혹은 SpringApplicationBuilder.listeners(...) 메서드를 이용하면 된다.
  만약에 리스너가 자동으로 등록되길 바란다면 프로젝트 내에 META-INF/spring.factories 파일을 추가하고 
  org.springfremework.context.ApplicationListener를 키로 해서 리스너들을 참조하도록 하면 된다.
  #Listener
  org.springfremework.context.ApplicationListener=listener.MyListener, listener.StartListener
  ```
  
  * 웹 환경
    * 웹 환경을 수동으로 설정하고자 한다면 setWebApplicationType 을 선언하면 된다.
    ```java
    @SpringBootApplication
    public class DemoApplication {
        public static void main(String[] args) {
            SpringApplication app = new SpringApplication(DemoApplication.class);
            app.addListeners(new ApplicationPidFileWriter());
            app.**setWebApplicationType**(WebApplicationType.SERVLET);
            //app.setWebApplicationType(WebApplicationType.NONE); JUnit 테스트할 때 유용하다.
            app.run(args);
        }
    }
    ```
  * 애플리케이션 실행인자 접근
    * SpringApplication.run(...)으로 전달되는 실행인자의 접근은 ApplicationArguments 빈을 이용한다.
    * option과 non-option 인자로 분류하여 접근할 수 있다.
    ```java
    @Slf4j
    @Component
    public class AppArgsAccessor {

        @Autowired
        public AppArgsAccessor(ApplicationArguments args) {
            boolean debug = args.containsOption("debug");
            log.debug("debug={}", debug);
            List<String> files = args.getNonOptionArgs();
            log.debug("files={}", files);
        }
    }
    ```
  * CommandLineRunner or ApplicationRunner 사용하기
    * SpringApplication과 함께 실행되도록 빈을 정의할 수 있는 인터페이스이다.
    * **애플리케이션이 실행될 때 반드시 한번 실행되어야 하는 기능을 구현**하는 데 사용할 수 있다.


### 오타
* p62(소스), //app.setWebEnvironment(false); (1) 이 있는데 이에 대한 설명이 없다. 아마도 deprecated 설명인 듯.

  
