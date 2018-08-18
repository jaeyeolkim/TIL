## 부트 스프링 부트 도서(챕터2)
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


### 오타
* p19(노트), 스프링 부트는 프로젝트 빌드도구로 그레이들**와** 메이븐 중에서 사용하길 권한다.(와 -> 과)
* p27(중간), spring-boot-depen dencies(공백이 들어가 있다)
* p28(중간), 개발자 로컬환경 CI 서버에 설치하지 않고 -> 개발자 로컬환경이나 CI 서버에 설치하지 않고
