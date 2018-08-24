HttpServlet
JSP
GET: Parameter를 Request 
`<% request.getParameter("cmd")%>`
이런 식으로 요청.
"cmd"는 내가 이름 붙이기 나름이다. 

웹 통신 HTTP 는 request/response로 이뤄져 있다.

jmf: 공통기능을 모아둔 것

AWS
OPEN API
HTTP API
REST API

**Eclipse에서 Git clone해서 프로젝트 열기**
Bitbucket에서 Git Repo 주소를 복사한다.

Eclipse 에서 Perspective 로 Git을 연다.

Eclipse-Git 에서 Clone Git 을 한다. 

Eclipse 에서 Perspective로 Java를 연다. (Package Explorer 탭이 나오도록)

Import - Project from.. Maven - Existing Project - Browse 후 선택

**여러 톰캣 서버 돌리기**
Servers 탭에다가 Tomcat-8.5 이상을 추가한다. 

Tomcat 별로 Add/Remove해서 Project를 한개씩 등록한다. 

Server1 - manager-web - 808x

Server2 - oauth - 808x

Server3 - api - 808x
- 각 서버별로 HTTP/1.1 포트 지정해주기.
- 각 서버별로 module 탭 --> path 지정 --> 더블클릭해서 Auto Enable 해제

*ERROR?*

톰캣 서버 돌리고 JDBC 에러 어쩌고가 나면 DB 권한접근 에러일 가능성이 있다. 권한이 없거나 DB 접속가능한 이용자 수를 초과했을 수 있다. 

*OR*

JDBC Driver가 없는 것이라면 mavenrepository 웹사이트에서 mysql-connector-java.jar 를 tomcat>lib 밑에 두면 된다. maven repository는  Users > .m2 폴더에 주로 있다. 

**2/3/4-tier**

PC (client) ----------- FE (WAS) ----------- BE/secured API (WAS)  -------- DB

                   manager-web                api 

                     |___ Access Token Oauth2.0 __|

                        |___   WEB SERVER  ___|


**Polymorphism**
- 다형성
- interface 쓰는 효과
- overloading: 같은 이름의 함수여도 인자가 다른 경우
- overriding: 슈퍼/상속한 클래스/인터페이스의 함수를 child가 재정의할 수 있는 것


**MVC**
Old: .php, .jsp 한페이지에 다 몰아넣기
New: MVC - model, view, controller

**Listener, Filter 란?**

Browser

filter
interceptor

controller
Rest-client...

filter
interceptor
controller

service
repo-class (DAO)

**Annotation**

@ResponseBody: 객체를 json으로 준다.

