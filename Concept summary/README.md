
<div align="center" id="top">
<img height="270px" width="270px" src="./logo.png"><br>
  <h1>📃개념 및 궁금증 정리</h1>
</div>

***
- 이클립스 Spring Tool Suite(STS) 설치 (Legacy Project 등 이전 버전의 부가기능을 사용하고자 할 때)
  - pring Tools 3 Add-On for Spring Tools 4 3.9.14(Spring framework 설치)
---

## 스프링 프레임워크(Spring Framework)이란
- POJO 프레임워크 중 하나이며 자바 플랫폼을 위한 오픈소스 애플리케이션 프레임워크로서 스프링(Spring)이라고도 불린다.
- 동적인 웹 사이트를 개발하기 위한 여러 가지 서비스를 제공한다. 

***

## POJO
  - 설명
    - 주로 특정 자바 모델이나 기능, 프레임워크를 따르지  않는 Java Object를 지칭
  - 특징
    1. 특정 규약(contract)에 종속되지 않는다. (Java 언어와 꼭 필요한 API 외에 종속되지 않는다.)
    2. 특정 환경에 종속되지 않는다.
    3. 객체지향원리에 충실해야 한다.
  - EX)
    - Java Bean 이 아닌 Getter 와 Setter 로 구성된 가장 순수한 형태의 기본 클래스

***

### 강한결합 
어떤 클래스의 유무나 로직 변경에 의해 다른 클래스에도 영향을 미친다.
### 약한결합
다른 객체의 의존하지 않고 인터페이스에 의존

## MVC 패턴
- 개발 할 때, 3가지 형태로 역할을 나누어 개발하는 방법론
- Model : 백그라운드에서 동작하는 로직을 처리한다.
- View : 사용자가 보게 될 결과 화면을 출력한다.
- Controller : 사용자의 입력처리와 흐름 제어를 담당한다.



## 프레임워크(Framework)
어떤 문제를 해결하기 위한 잘 설계된 재사용이 가능한 코드(모듈)들의 집합을 말합니다
      

## IoC(Inversion of Control) - 제어의 역전
- 기존 : 객체 결정 및 생성 -> 의존성 객체 생성 -> 객채 내의 메소드 호출
- IOC : 제어의 흐름을 사용자가 컨트롤 하지 않고 위임한 특별한 객체에 모든 것을 맡기는 것

### IoC는 DI와 DL에 의해 구성 
  - DL(Dependency Lookup) - 의존대상(사용할 객체)을 검색(lookup)을 통해 반환받는 방식
    - factory.getBean(id); 내가 찾고자 하는 대상을 검색해서 객체를 확보한다

  - DI(Dependency Injection) - 의존대상(사용할 객체)을 주입을 통해 받는 형식
    - Service 계열에서 DAO를 필요로 한다. 즉 의존관계(has a 관계)가 있다.
    - Service(DAO) 이것을 의존성을 주입하는 것이다.


***

<div align="center" id="top">
  <h1> ✏️어노테이션(Annotation)</h1>
</div> 

- @Modelattribute
    - @Modelattribute를 사용하면 @RequestParam으로 파라미터를 1:1로 받지 않고 한꺼번에 받을수 있다는 장점이 있다.
    - 해당 클래스의 각각 해당변수의 setter를 통해서 해당 멤버 변수로 binding된다.
    - 해당 클래에 setter가 반드시 존재햐아한다. 
- @Component : 해당 클래스가 스프링에서 객체로 만들어서 관리하는 대상임을 명시하는 어노테이션
- @ComponentScan : @Component가 있는 클래스를 스프링이 읽어주도록 하는 어노테이션
- @Autowired : 객체를 자동으로 주입하는 어노테이션
- @Autowired(required=false)  // required를 false로 하여 주입 안받아도 예외처리 하지 않도록 함. // 기본값은 true
- @Qualifier : 사용할 의존 객체를 선택할 수 있도록 해준다.
- @RequestParam
  - 표현 방식 : @RequestParam("가져올 데이터의 이름")[데이터타입][가져온데이터를 담을 변수]
  - required=false : 키값이 존재하지 않아도 에러발생 X
  - defaultValue : 값이 존재하지 않다면 넘어가는 default값 설정
- @Valid 
    - @NotNull	Null 불가(int는 안됨 -> 해결방법: Integer, double, float)
    - @Null	Null만 입력 가능
    - @NotEmpty	Null, 빈 문자열 불가(int는 안됨 -> 해결방법: Integer, double, float)
    - @NotBlank	Null, 빈 문자열, 스페이스만 있는 문자열 불가
    - @Size(min=,max=)	문자열, 배열등의 크기가 만족하는가?
    - @Pattern(regex=)	정규식을 만족하는가?
    - @Max(숫자)	지정 값 이하인가?
    - @Min(숫자)	지정 값 이상인가
    - @Future	현재 보다 미래인가?
    - @Past	현재 보다 과거인가?
    - @Positive	양수만 가능
    - @PositiveOrZero	양수와 0만 가능
    - @Negative	음수만 가능
    - @NegativeOrZero	음수와 0만 가능
    - @Email	이메일 형식만 가능
    - @Digits(integer=, fraction = )	대상 수가 지정된 정수와 소수 자리 수 보다 작은가?
    - @DecimalMax(value=) 	지정된 값(실수) 이하인가?
    - @DecimalMin(value=)	지정된 값(실수) 이상인가?
    - @AssertFalse	false 인가?
    - @AssertTrue	true 인가?

***

## AOP
- 핵심 기능과 공통 기능을 분리시켜놓고, 공통 기능을 필요로하는 핵심 기능들에서 사용하는 방식
- 즉 핵심기능과 공통 기능을 분리시킨다.


## dispatcher-servlet <br>
- Servlet Container에서 HTTP프로토콜을 통해 들어오는 모든 요청을 프레젠테이션 계층의 제일앞에 둬서 중앙집중식으로 처리
- Front Controller와 같은 개념
- 기존 -> url당 servlet을 생성하고 그에 맞는 Controller에게 요청을 보내주는 코드를 각각 따로 작성
- dispatcher servlet을 통하여 모든 요청을 한곳에서 받아서 처리



## Maven
- 자바용 프로젝트 관리도구로 Apache Ant의 대안으로 만들어졌다.
- 필요한 라이브러리를 특정 문서(pom.xml)에 정의해 놓으면 내가 사용할 라이브러리 뿐만 아니라 해당 라이브러리가 작동하는데에 필요한 다른 라이브러리들까지 관리하여 네트워크를             통해서 자동으로 다운받아 준다.



## mybatis 
- Mybatis는 자바 오브젝트와 SQL사이의 자동 매핑 기능을 지원하는 ORM(Object relational Mapping)프레임워크이다.
- SQL을 별도의 파일로 분리해서 관리하게 해준다.
Hibernate나 JAP(Java Persistence Api)처럼 새로운 DB프로그래밍 패러다임을 익혀야하는 부담 없이 SQL을 그대로 이용하면서 JDBC코드 작성의 불편함도 제거해주고 도메인 객체나 VO객체를 중심으로 개발이 가능하다는 장점이 있다.
***
- xml 문서내 id 속성은 unique해야합니다.
다른 xml 무서간에 동일한 id 속성이 있을 수 있으므로
네임 스페이스 개념을 사용합니다.

## typeAlias
- 보통 mybatis xml 파일에 쿼리문을 작성할 때 parameterType 과 resultType을 적어 파라미터의 자료형과 반환 타입의 자료형을 적는다.
- 이러한 타입명이 복잡한 경우 typeAlias를 이용하여 간결하게하고 오타를 줄일수 있다.
- 표현방식 : '<'typeAlias alias="testVO" type="com.test.testVO"/'>'
  - alias = 별칭 / type = 클래스 경로
***
## Mapper
- Mapping 파일에 기재된 SQL을 호출하기 위한 인터페이스
- MyBatis 3.0 이상부터 지원
- 간단한 XML Statements를 사용해서 java beans를 SQL statement에 맵핑시킨다.
 
 ***
## Message tag
- message tag를 이용하여 미리 저장된 단어나 문장을 가져와서 사용할 수 있다.
      
        <spring:message/>
        
        ///////Message Tag를 사용하기 위해 가장 먼저 MessageSource를 등록해야 합니다.
        <bean id="messageSource" class="org.springframework.context.support.ResourceBundleMessageSource" p:basename="ApplicationResources" />

        ///////jsp에서 taglib를 등록
        <%@ taglib prefix="spring" uri="http://www.springframework.org/tags" %>

        ///////Property File
        MSG.HTML.MYCODE=내코드
        MSG.HTML.OUR_CODE=우리코드

        ///////JSP상의 작성법 <spring:message code="MSG.HTML.MYCODE"/>

## ModelAndView
- 데이터를 전송시킬 수 있는 리턴 타입
  - setViewName : 어떤 페이지를 보여줄 것인지
  - addObject : key와 value를 담아 보낼 수 있는 메서드

- Model, ModelMap Vs ModelAndView 차이점
  - Model, ModelMap -> 데이터만 저장한다.
  - ModelAndView -> 데이터와 이동하고자 하는 View Page를 같이 저장한다
      

## pom.xml
- POM(Project Object Model)을 설정하는 부분으로 프로젝트 내 빌드 옵션을 설정하는 부분이다.
- 프로젝트에 필요한 모든 라이브러리를 관리
    
    
## redirect와 forward방식의 차
#### redirect는 처음 요청한 URL과 리다이렉트가 일어난 후의 URL이 다르게 변경된다는 점이다. forward는 요청 URL로 동작된 후에도 같다.  

<img height="270px" width="450px" src="./forward.png"><br>

<img height="270px" width="450px" src="./redirect.png"><br>

## ERROR 코드
- 중요한 몇몇 에러 코드 정리
- 200 : 에러 없이 성공적으로 페이지를 불러오거나 데이터를 전송
- 400 : Bad Request로써, 요청 실패-문법상 오류가 있어서 서버가 요청 사항을 이해하지 못함
- 404 : Not Found, 문서를 찾을 수 없음->클라이언트가 요청한 문서를 찾지 못한 경우에 발생함 (URL을 잘 살펴보기)
- 405 : 	Method not allowed, 메소드 허용 안됨-> Request 라인에 명시된 메소드를 수행하기 위한 해당 자원의 이용이 허용되지 않았을 경우 발생함.    (페이지는 존재하나, 그걸 못보게 막거나 리소스를 허용안함)
- 415 : 지원되지 않는 형식으로 클라이언트가 요청을 해서 서버가 요청에 대한 승인을 거부한 오류를 의미한다.
(ContentType,Content Encoding 데이터를 확인할 필요가 있다.)
- 500 : 서버 내부 오류는 웹 서버가 요청사항을 수행할 수 없을 경우에 발생함
- 505 : HTTP Version Not Supported



## 하나의 Form에 여러개의 submit

```
<form method="post" name="form">
    <input type="submit" value="조회" onclick="javascript: form.action='<%=request.getContextPath()%>/update.cd';"/>
    <input type="submit" value="조회" onclick="javascript: form.action='<%=request.getContextPath()%>/delete.cd';"/>
</form>
```
- 참고 주소 : https://kutar37.tistory.com/entry/%ED%95%9C%EA%B0%9C%EC%9D%98-Form%EC%97%90%EC%84%9C-%EC%97%AC%EB%9F%AC%EA%B0%9C-Submit-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0
