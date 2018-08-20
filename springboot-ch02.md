## 부트 스프링 부트 책(챕터2)
### 스프링 부트 살펴보기

* 의존성 관리
  * 스프링 부트는 프로젝트 빌드도구로 그레이들과 메이븐 중에서 사용하길 권한다.
* 스타터
  * 스타터는 애플리케이션이 이용할 수 있는 의존성을 기술하고 있는 집합체이다. 필요한 기능을 가진 의존성 라이브러리를 모두 기술하지 않아도 관련된 의존성 라이브러리를 한번에 담을 수 있다.
  * 스타터는 동일한 네이밍 패턴을 따른다.
    * spring-boot-starter-*
* spring-boot-starter-parent 없이 사용하기
  * 모든 메이븐 구성을 명확하게 선언하기를 원하는 경우, 의존성 관리(플러그인 관리는 안됨)의 장점은 유지하고 싶다면 <scope>import</scope> 를 추가한다.
  * 하지만 이 설정은 속성(property)을 이용한 개별적인 의존성을 재정의 할 수 없다.
  * 부모 스프링 부트 스타터 상속에서 프로퍼티만 정의했던 것과 동일한 결과를 얻기 위해서는 dependencyManagement 엔트리 안에서 spring-boot-dependencies 엔트리 이전에 필요한 것을 추가해야 한다.
* spring-boot-starter-parent 는 java.version 이 1.6 이다. java.version을 추가하여 변경한다.
  ```
  <properties>
    <java.version>1.8</java.version>
  </properties>
  ```
* 래퍼(Wrapper)
  * Gradle을 각 개발자나 CI 서버에 깔지 않고, 프로젝트에 함께 포함시켜 배포할 수 있는 방법을 제공해준다.
  * 자세한 설명은 http://kwonnam.pe.kr/wiki/gradle/wrapper
* 코드 구조
  * 애플리케이션 메인 클래스는 최상위 패키지(kr.co.~)에 위치하는 것을 권장한다.
  * 최상위 패키지에 있는 클래스에 @ComponentScan를 선언하면 basePackage 속성을 정의할 필요가 없다.
  * **SpringBootApplication(메인 클래스) 의 위치가 (app 하위등으로)변경되면 scanBasePackages 속성에서 탐색해야 할 패키지를 지정해야 하는 번거로움이 생긴다.**
  * 메인 클래스 위치를 임의로 변경하고 애플리케이션이 실행되지 않는다고 하는 경우가 제법 많으니 주의하자.(빈을 탐색하지 못해 예외가 발생)
* 구성(Configuration) 클래스
  * 스프링 부트는 자바기반 구성(JavaConfig)을 선호한다.
  * XML 소스를 이용하는 것도 가능하지만 기본적으로는 @Configuration과 자바코드로 선언하는 것을 권장한다.
  * 모든 것을 @Configuration이 선언된 하나의 클래스에 몰아 넣을 필요는 없다.
  * @Import 애너테이션을 이용하여 추가적인 구성 클래스를 불어와 사용할 수 있다.
  ```
  @Configuration
  @Import(EnableWebMvcConfiguration.class)
  ```
  * 이에 대한 대안으로 @ComponentScan을 사용하면 @Configuration를 포함한 모든 스프링 컴포넌트를 사용할 수 있다.
  * XML 구성 불러오기는 @ImportResource 의 인자로 XML의 위치를 지정하면 된다.
* 자동구성(auto-configuration)
  * 의존성을 기반으로 자동구성한다.
  * 예를 들어 h2database 라이브러리가 클래스패스 상에 존재한다면 알아서 인-메모리 데이터베이스로 자동구성한다.
  * 자동구성 기능을 활성화하려면 @Configuration이 선언된 클래스에 @EnableAutoConfiguration 또는 @SpringBootApplication을 추가하면 된다.
  * @SpringBootApplication은 @EnableAutoConfiguration 과 @SpringBootConfiguration을 하나로 합친 애너테이션이다.
  * 자동구성된 특정 부분을 재정의하고 시작하는 것이 가능하다. 예를 들어, DataSource 빈을 추가하면, 기본 내장 데이터베이스 지원은 비활성화된다.
  * 현재 제공되는 자동구성은 스프링부트 시작 시 --degbug 를 활성화하면 된다.
  * 자동구성 일부 비활성화 3가지 방법
    * @EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})
    * 클래스패스 상에 없는 경우(추후 영향을 끼칠 수 있는) @EnableAutoConfiguration(exclude={"org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration"})
    * application.yml 에서 spring.autoconfigure.exclude 속성에 정의
* @SpringBootApplication 이용
  * @Configuration, @EnableAutoConfiguration, @ComponentScan 이 세개를 함께 사용한 것과 동일하다.
* JAR로 패키징된 애플리케이션은 컨테이너가 포함되기 때문에 즉시 실행이 가능하다.
  * IDE - 메인 클래스를 Run 'SpringBootApplicaton' 실행
  * java -jar boot.jar
  * gradle, maven 등으로도 실행
* 스프링 부트 개발자도구
  * spring-boot-devtools 모듈은 개발할 때 필요한 기능들을 제공한다.
  * 패키징된 애플리케이션이 실행될 때 자동으로 비활성화된다. java -jar 또는 별도의 클래스로더를 통해서 시작하면 운영으로 판단한다.
  * 템플릿 엔진인 타임리프를 개발시에만 적용하고자 한다면 spring.thymelear.cache 속성을 정의할 수 있다.
  * 클래스패스 내에 파일 변경시 자동으로 재시작된다.
  * 인텔리제이는 빌드(Build -> Make Project)시 재시작된다. 저장시 재시작하려면 매크로를 이용해야 한다.(sbcoba.tistory.com/36)
  * 재시작은 껐다 켜는 것에 비해 매우 빠르게 처리된다.
    * 기본 클래스로더와 재시작 클래스로더가 있는데, 개발하는 과정에서 변경된 클래스는 재시작 클래스로더에 적재되어 있다.
    * 재시작될 때 기존 재시작 클래스로더를 없애고 새로운 것을 만든다.
    * 기본 클래스로더가 유지되고 필요한 것들을 가지고 있기 때문에 빠르다.
  * 재시작 대상 제외
    * spring.devtools.restart.exclude: static/**,public/**
    * spring.devtools.restart.additional-exclude 을 사용하면 기본 제외목록을 유지하면서 추가적으로 제외할 수 있다.
  * 재시작 비활성화
    * spring.devtools.restart.enabled 속성을 정의
  * 홈디렉토리에 '.spring-boot-devtools.properties' 이름의 파일을 추가하면 개발자도구에 대한 전역설정을 할 수 있다.

### 오타(어색한 부분)
* p19(노트), 스프링 부트는 프로젝트 빌드도구로 그레이들**와** 메이븐 중에서 사용하길 권한다.(와 -> 과)
* p27(중간), spring-boot-depen dencies(공백이 들어가 있다)
* p28(중간), 개발자 로컬환경 CI 서버에 설치하지 않고 -> 각 개발자 로컬환경이나 CI 서버에 설치하지 않고
* p31(중간), basePa**kc**age -> basePa**ck**age
* p42(끝), 애플리케이션을 컨테이너**를** 함께 JAR로 패키징하면서(를 -> 와)
