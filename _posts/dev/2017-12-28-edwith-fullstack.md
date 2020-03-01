---
layout: post
categories: dev
title: "edwith 웹 개발 공부"
date: 2017-12-28T13:01:27-05:00
share: true
---

공부자료출처: http://www.edwith.org/boostcourse-web

# [2] DB 연결 웹 애플리케이션

## 0. 소개

frontend
- javascript
- dom
- event
- ajax

backend
- jsp: servlet 로 바뀌어서 동작한다.
- servlet
- database: mysql, java jdbc, spring jdbc


## 1. 자바스크립트

1. 기초
- == 와 === 차이
- 타입은 선언할 때가 아니라 실행할 때 결정된다. 
    - toString.call 결과 매칭시 사용
    - typeof: 문자/숫자에 사용
    - isArray: 배열에 사용

2. 비교 반복 문자열
- if, switch: 분기문
- for, while: 반복문
- 문자열 조작 메서드 (중요!)
    - .split(","): ,를 기준으로 자른다
    - .replace(".", "$"): .를 $로 바꿔준다.
    - .trim(); 불필요한 끝의 공배들을 줄여준다.

3. 자바스크립트 함수
- 함수: 호이스팅 hoisting: 함수 안의 변수 값들을 미리 다 모아서 선언을 먼저 한다. 
    - 호이스팅으로 선언이 되었지만, 값이 할당되기 전에 실행하면 undefined가 반환된다. 
- 함수: 반환값과 undefined
    - 자바스크립트는 반드시 return값이 존재하며, 없을 때는 기본 반환값인 undefined 반환.
    - void 타입은 없다.

- arguments (지역변수) 객체
    - 함수: 선언한 인자보다 더 많이 받을 수 있음.
    - 이때. 넘어온 인자를 arguments 배열의 형태로 접근.
    - arguments가 배열 타입은 아니다. 배열 메소드 사용 불가.


```js
// 연습문제
// 참조: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce
// 참조2: https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/arguments
// 참조3: https://stackoverflow.com/questions/38566788/return-sum-of-all-arguments-passed-to-function


function print(){
    const args = Array.from(arguments);
    console.log(args);
    const argsArr = [...arguments];
    console.log(argsArr);
}

print(1,2,3,4,5);

function sum(...args){
    const result = [...args].reduce((accumulator, currentValue) => accumulator+currentValue);
    // .reduce( (a,b) => a+b, 0); 가능
    // accumulator의 시작이 0 이라는 소리
    console.log(result);
}

sum(1,2,3,4,5);
```

## 2. WEB UI 개발

### 1) window 객체 (setTimeout)
- windows 객체
    - setTimeout, alert 같은 것들은 부를 때 windows.을 생략해도 된다. 
        - 전역 객체이기 때문에.
    - setTimeout 실행은 비동기이다.
    - setTimeout 안의 함수는 콜백 함수라고 생각하면 된다.
        - 인자로 함수를 받고, 나중에 실해되는 함수를 콜백함수라고 보통 부른다.
        - 자바스크립트는 함수를 인자로 받을 수 있고, 함수를 반환할 수도 있다. 

```js
function run() {
    console.log("run start");
    setTimeout(function) {
        var msg = "hello edwith";
        console.log(msg);
        console.log("run...ing");
    }, 2000);
    console.log("run end");
}
// start, end가 먼저 출력되고
// 2초 후에 setTimeout 내부 문장이 출력됨
```

> 참조 setInterval: https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setInterval

### 2) DOM과 querySelector
- DOM: html코드를 브라우저에서 저장하는 형태: 객체 형태의 모델 Document Object Model
- DOM Tree 안에 정보들이 다 저장되어 있음
    - document - root element (html) - element (a / body) - attribute (href) / text (h1)
- 자바스크립트로 DOM Tree 탐색 알고리즘 구현하면 너무 힘들어서 DOM API가 제공하는 메소드를 이용
    - getElementById()

- querySelector() 사용법
    - tag: <code>document.querySelector("a");</code>
    - id: <code>document.querySelector("#nav-cart-count")</code>
    - class: <code> document.querySelector(".nav-line-2")</code>
    - class inside tag: <code>document.querySelector("body .nav-line-2");</code>
    - class(nav-arrow) inside class(nav): 
    <code> document.querySelector(".nav > .nav-arrow");</code>
    - attribute of elements: <code>document.querySelectorAll("iframe[data-src]")</code>

- querySelectorAll 활용해보기: https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll


- css selector 문법: querySelector, querySelectorAll 메서드에서 사용가능

### 3) Event 

- HTML element별로 이벤트 생각하기
- .addEventListener( 이벤트 이름, 함수)
    - 함수: 이벤트가 발생하면 가동되는 함수: Event Handler/ Event Listener
    - 콜백함수는 이벤트가 발생하면 실행된다.

- 이벤트 리스너 안에서 이벤트객체를 활용하여 추가적인 작업 가능
    - event.target: 이벤트가 발생한 element 알려줌
    - element도 객체이므로 갖고 있는 속성 (event.taget.nodeName, classname ...) 사용가능
- 참고: https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#Event_handler_properties, https://developer.mozilla.org/en-US/docs/Web/Events

### 4) Ajax (XMLHTTPRequest) 통신의 이해

- 브라우저 새로고침 없이 서버로부터 데이터를 받기 위해 이용한다.
- 동적으로 필요한 시점에 컨텐츠를 받아온다.
- 다양한 포맷의 데이터를 주고받을 수 있다 (주로 JSON)
- 실행 코드: XMLHTTPRequest 객체를 사용하는 표준방법이다.
    - 객체 생성 --> open 메서드로 요청 준비 --> send 메서드로 서버 보내기

```js
// 비동기 로직 이해하기

// 1. XMLHTTPrequest 객체 생성
var oReq = new XMLHttpRequest();
//서버에서 응답이 오면 (요청처리 완료되면)
// load 이벤트 발생
oReq.addEventListener("load", function(){
    //콜백함수 실행
    // 이때 ajax 함수는 반환하고 call stack 에서 사라진 상태
    console.log(this.responseText);
}); 

// 2. open 메소드로 요청 준비
oReq.open("GET", "./json.txt");
// 3. 서버로 보내기
oReq.send();
```


## JSP

#### JSP 라이프싸이클 기초
- init, service, destroy 메소드 ...
- JSP 파일 생성: 이클립스 -> Dynamic Web Project로 생성한 webdemo 프로젝트 -> WebContent 폴더 -> WEB-INF 폴더 -> something.jsp 
- JSP는 Servlet으로 바뀌어서 (Servlet소스로 자동 컴파일되어서) 돌아간다고 했지?
- something_jsp.java로 바껴있는 파일을 찾을 수 있다. 
- 이 파일의 경로는... your_eclipse_workspace_name\.metadata\.plugins\org.eclipse.wst.server.core\tmp1_or_tmp0\work\Catalina\localhost\your_project_name\org\apache\jsp
- 네가 jsp에 짠 코드는 jspService() 메소드에 들어가 있다.

**실행순서**
1. 브라우저가 웹서버에 JSP에 Request 신호  보냄
2. 웹서버가 최초로 JSP 를 내보내는 경우, 
- JSP 코드 --translation--> Servlet 코드
- Servlet 코드를 Compile해서 실행가능한 bytecode로 변환 & (..-jsp.java 파일) class 파일 생성.
- Servlet class를 로딩, 인스턴스를 생성.
3. 서블릿이 실행되어 request 처리하고, response 를 생성한다. 



- 


## API
- 페이스북 로그인 / 네이버 로그인 이런 설정들을 본 웹사이트 외부에서 진행 하는 경우, API를 써서 연동될 수 있게 한다. 

### 그래서 REST API 가 뭐야?
[그런 rest api로 괜찮은가](https://www.youtube.com/watch?time_continue=208&v=RP_f5dMoHFc)
- 로이 필딩: HTTP 통신에 대한 고민: how do i improve http without breaking internet
  - HTTP Object Model --> 후에 REST 라는 이름으로 발표
  - REpresentational State Transfer: "Architectural Styles and the Design of Network-based Software Architectures"

- API
  - REST API : Flickr 에서 API 최초 공개
  - 
