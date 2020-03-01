---
title: "java: spring framework 인프런 스터디"
layout: post
categories:
  - dev
tags:
  - dev
  - java
  - spring
date: 2018-08-08T13:01:27-05:00
last_modified_at: 2018-08-08T13:01:27-05:00
---

0. 스프링 프레임워크란 무엇인가

주요기능: DI, AOP, MVC, JDBC
기존의 프로그래밍에서 구조 만들어나가는 방법론들.
스프링: 자바 기반. 웹 어플리케이션에 적용
자바로 데이터베이스에 통신하는 방법. MVC - 웹 구조화 시키는 방법
DI - 주입 기능. 어떤 기능을 모듈로 만들어서 주입. 
AOP - 관점 지향. 공통된 부분은 모듈화해서 뗏다 붙였다 하기.

프레임워크: 개발자들이 업무를 하기 전에 어떤 작업을 할지 추상적으로 만든 틀. 

틀의 각 모듈: core, aop, jdbc, tx, webmvc
- core: 핵심인 DI, IoC
- aop:  공통 기능 따로 뽑아서 개발
- jdbc: 자바와 데이터베이스 통신
- tx: 트랜잭션
- webmvc: 컨트롤러, 뷰 이용한 스프링 MVC 구현 기능 제공
스프링 프레임워크에서 제공하는 모듈사용하려면, 의존설정을 개발 프로젝트에 xml 파일 이용해서 개발자가 직접 하면 된다.

IoC: 스프링 컨테이너
스프링에서 객체를 생성하고 조립하는 컨테이너. 컨테이너를 통행 생성된 객체가 Bean.
XML: 객체 생성 및 속성 데이터 작성 --> 스프링 컨테이너 [내부: XML 이용해서 만들어진 객체 - 빈 생성 및 조립] --> 개발문서(자바 파일들): 스프링 컨테이너에 있는 빈들을 꺼내서 그때 그때 필요할 때 사용하여 애플리케이션/기능 구현.



1-1. 스프링 프로젝트 생성

Maven을 사용해서 스프링 프로젝트를 생성해보자.
pom.xml : 스프링의 각 기능-모듈들 - core/jdbc/aop 등을 가져오기 위한 파일.
- dependencies - artifact,version,group, 
- build에 필요한 기능들 명시: plugins - artifact, version,configuration 등

에러: JRE 라이브러리 버젼이랑 안맞는다!!
- Maven > Update Project 해서 버젼을 맞춰주라

폴더 구조 이해하기.
- 기본적인 원리 > 디렉터리 구조, 파일의 역할 이해하기
- src > main > java: 자바언어로 프로그래밍, 기능 구현: 자바 파일 관리
- src > main > resources: 프로젝트 빌드, 개발환경에 관한 여러가지 파일들: 자원파일 관리, xml, properties, 스프링 설정 파일들이 저장된다.

1-2. 스프링 프로젝트 처음 시작

- Maven project 생성 > artifact 설정: spring4 입력 (pom.xml 에 추가됨) > 
- 자바를 기반으로 한 프레임워크
- 일반 자바: 순수 자바어로만 프로젝트
- 스프링 프레임워크: 메인 리포에서 스프링 모듈들을 사용 - pom.xml 

리소스 폴더 > applicationContext.xml
스프링은 컨테이너IoC 큰걸 만들고 그안에 객체를 다 생성하고, 거기서 필요한 걸 빼와서 사용하는 방식. 그 객체를 만들어주는게 applicationContext.xml (스프링 컨테이너 생성)
bean 태그 (객체 생성)

resources > new : xml file, applicationContext.xml
beans 
id
class: 
new 키워드로 자바에서 객체 생성
<bean id="anyname" class="projectname.mainclassname" /> xml 로 객체 생성 - 메모리에 저장 꾺
MainClass.java 
에서 new 생성자를 아예 쓸 필요가 없음 이제

어플리케이션 컨텍스트에서 만들어준 스프링 컨테이너를 접근해볼까? 어떻게?
GenericXmlApplicationContext ctx = new GenericXml~~~~("classpath:applicationContext.xml")
Xml 을 가져오는 메소드

컨테이너를 가져왔으니 그 안의 객체-빈을 가져오기
ctx.getBean(beanId, DataType)

TransportationWalk transportationWalk = ctx.getBean("anyname", TransportationWalk.class)
 
 tr--Walk.move();

 ctx.close();


 xml 파일 이용해서 컨테이너,객체 생성
 이거를 접근하는 방법~ xml 가져오는 클래스를 이용, 자원 출처를 적고,
 transportationWalk 객체를 가져온 부분
 xml 이나 annotation 이용해서 대부분 객체 생성하고 다룸.


 자바 폴더, 코딩 파일, 자원들이 보이는 것, 



## 의존 객체

2-1. DI Dependency injection 의존 주입
DI 이용한 프로그래밍 방법. 스프링 DI 설정 방법

DI = OOP 프로그래밍의 방법론 중 하나
자바 언어를 했었고, JSP 했고, 안드로이드를 했다면, 의존주입 경험이 있을 것.

예시) 자동차 장난감과 배터리
- 배터리 일체형: 배터리 없으면 새로 구입 ㅠㅠ
- 배터리 분리형: 교체 가능하다. 

객체 지향 프로그래밍 만들 때 생각해서 대입.
- 객체 하나만 교체하고 싶다. 
- +, -, %, * 객체들 별로 다를텐데 일체형으로 만들면 어떤 것은 못쓸수도있음.
- 배터리는 인터페이스로 만들고, 충전지/전기/ 등 다양한 타입의 배터리로 구현하라.

유연성: OOP 
- 객체를 독립화 시켜서 (Interface)
- 유연하게 띄었다 붙였다...
- Dependency Injection 얘기도 연장선상에 있다. 
  - 배터리를 주입하는 격.

코드.
```java
//배터리 일체형
public class ElectronicCarToy {
    private Battery battery;
    public ElectronicCarToy() {
        battery = new NormalBattery();
    }
    //생성자에서 객체를 주입.
}
```

```java
// 배터리 분리형 [1]
public class ElectronicRobotToy {
    private Battery battery;
    public ElectronicRobotToy(){}
    public void setBattery(Battery battery){
        this.battery = battery;
    }
    //setter 에서 주입 (1)
}
```

```java
// 배터리 분리형 [2]
public class ElectronicRobotToy {
    private Battery battery;
    // 생성자에서 디폴트로 처음에 넣어줌 (1)
    public ElectronicRobotToy(Battery battery){
        this.battery = battery;
    }
    public void setBattery(Battery battery){
        this.battery = battery;
    }
    // setter를 이용해서도 배터리 교체 가능 (2)
}
```

스프링 설정 방법
- 객체는 어차피 다 스프링 컨테이너에 다 모여있다.
- applicationContext.xml --> GenericXML``` method --> spring Container 에 Bean 객체들 [객체 안의 객체도 가능] --> getBean() -- Bean 객체를 필요로 하는 로직. 
  - 큰 객체에 작은 객체들이 있는 것들: Dependency Injection

클래스 구조
- 주입: 큰 객체에서 작은 객체를 만들 때, 객체를 애초에 처음부터 넣어줌. (파라미터 넣듯이)
```java
public StudentAssembler() {
  studentDao = new StudentDao();
  registerService = new StudentRegisterService(studentDao);
  deleteService = new StudentDeleteService(studentDao);
  selectService = new StudentSelectService(studentDao);
}
//생성자에서 studentDao 객체를 각 Service 객체에다가 처음부터 넣어줬음
// 같은 Dao를 Service 에 넣어줬으니, 쓰는 디비, 메소드들이 다 같음

```
- 스프링이니까 new 쓰지 말고, applicationContext.xml 에서 객체 컨테이너 사용하기
```xml
<bean id = "studentDao" class="ems.member.dao.StudentDao"></bean>
<bean id = "registerSerivce" class= "ems.member.service.StudentRegisterService"><constructor-arg ref="studentDao"></constructor-arg>
</bean>
```

## 의존 객체 주입 다양한 방법
- 생성자를 이용한 의존객체 주입
- setter 이용
- list 타입 의존 객체 주입
- Map 타입 객체 주입

 1. 생성자 이용
 
 ```xml
 <bean id="" class="" > // new 생성자와 마찬가지
 <constructor-arg ref=" "> // 객체 주입 (파라미터와 마찬가지)
 ```

 2. setter

```java
public void setJdbcUrl (String jdbcUrl) {
     this.jdbcUrl = jdbcUrl;
 }
setUserId { this.userId = userId;}
setUserPw {this.userPw = userPw;}
```
setter 메소드는 property로 대체.
set메소드 이름에서 set은 빼고 name,
파라미터를 value 속성값으로 바꿔서 xml에 쓰기
```xml
<bean id="" class="">
<property name="jdbcUrl" value="jdbc:oracle:thin:@localhost:1521:xe" />
<property name="userId" value="scott" />
<property name="userPw" value="tiger" />
```

3. list 타입 
```xml
<property name="devNames">
<list>
<value>Cherry</value>
<value>Terry</value>
<value>Henry</value>
</list>
</property>
```

4. Map 타입
```xml
<property class="admins">
<map>
<entry>
<key> <value>Cherry</value> </key>
<value>cherry@admin.com</value>
</entry>

<entry>
<key> <value>Terry</value> </key>
<value>Terry@admin.com</value>
</entry>
</map>
</property>
```


## 스프링설정파일분리

> 스프링설정파일을 분리하자
> 빈의 범위를 알아보자

applicationContext.xml : 설정파일
- appCtx1.xml: Dao 와 서비스객체
- appCtx2.xml : 데이터베이스 커넥션 관련
- appCtx3.xml : 앱 인포메이션 관련

이렇게 분리해보았다.

**여러 파일을 어떻게 불러오지?**

1. 스트링 배열
```java
String[] appCtxs ={"classpath:appCtx1.xml", "classpath:appCtx2.xml", "classpath:appCtx3.xml"}

GenericXmlApplicationContext ctx = new GenericXmlApplicationContext(appCtxs);
```
빈 객체를 다 메모리에 로드

2. 쪼갠것 중의 하나에다가 나머지를 import 시켜놓고 걔를 자바 파일에서 부르기
```xml
<!--appCtximport.xml-->
<import resource="classpath:appCtx2.xml">
<import resource="classpath:appCtx3.xml">
<!--Dao 내용들~~ -->

```
```java
//자바 파일
//import 할때 appCtximport.xml 만 해주면 됨
String appCtx = "classpath:appCtximport.xml";
```

**빈의 범위**
- Singleton: 싱글튼
  - getBean() 메소드로 호출될 때는 객체를 참조하는 것.
  - Spring Container에 객체를 생성해 놓는데, 동일한 객체는 1번만 생성된다.
  - (같은 객체들이 여러개 있는게 아니다)

- Prototype: 프로토타입
  - bean 생성할 때 `scope="prototype"`이라고 설정한다.
  - getBean() 메소드로 호출할 때마다 (똑같은 내용의) 다른 객체가 생성이 되서 받는다.  

## 의존객체 자동 주입
> constructor-org/property 이런 의존 설정 따로 수동으로 안하고 자동 주입하는 방법. 

> Autowired, Resource annotation

**자동주입 @Autowired**
- 주입하려고 하는 객체의 타입이 일치하는 객체를 자동으로 주입한다. 
- xml 코드가 간단해짐. 
- 디폴트 생성자 하나 미리 만들어야 함.

```xml
<context:annotation-config /> <!--이거 써줘야됨-->
<bean id="wrodDao" class="com.word.dao.WordDao" />
<bean id="registerService" class="com.word.service.WordRegisterService" />
```

```java
public class WrodRegisterService {
    
    // @Autowired  
    private WordDao wordDao;

    public WordRegisterService(){
        //위에 WordDao에 Autowired 할거면 기본 생성자 필요. 
        // 이것도 없으면 autowired가 끌어올 wordDao 생성자체가 안되어 있어서.
    }
    @Autowired
    public WordRegisterService(WordDao wordDao) {
        this.wordDao = wordDao;
    }
}
```

**자동주입 @Resource**
- 객체의 타입을 보는게 아니라 객체 이름을 보고 주입해준다.
- wordDao 랑 동일한 이름 `<bean id="wordDao"... />` 인 애를 찾는다.
