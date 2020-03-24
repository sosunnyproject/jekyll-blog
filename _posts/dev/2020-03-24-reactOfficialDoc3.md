---
layout: post
categories: dev
title: "REACT JS 공식 문서 파헤치기 (3)"
date: 2020-03-24T14:01:27-05:00
last_modified_at: 2020-03-24T14:01:27-05:00
share: false
---

### **목표: 리액트 공식문서를 120% 활용할 수 있게끔 익숙해지기**
- https://reactjs.org/docs/hello-world.html
- https://reactjs.org/tutorial/tutorial.html 

## [Chapter 6](https://reactjs.org/docs/handling-events.html)

### 1. React 엘리먼트 이벤트 핸들링은 DOM 엘리먼트 이벤트 핸들링과 몇 가지 문법 차이만 빼면 매우 유사하다.

- camelCase 사용
- jsx 는 이벤트 핸들링 string 이 아닌 function을 넘긴다.
- preventDefault 하기 위해 false를 리턴할 수 없다. preventDefault를 명시적으로 호출해야 한다. 

```js
// 1. function, not string
// instead of "activateLasers()"
<button onClick={activateLasers}> 
    Activate Lasers 
</button>

// 2. preventDefault
// instead of 
// <a href="#" onclick="console.log('The link was clicked.'); return false">

function ActionLink() {
    function handleClick(e) {
        e.preventDefault();
    }
    return(
        <a href="#" onClick={handleClick}>
            Click This!
        </a>
    )
}
```

- 여기서 e 는 [synthetic event](https://reactjs.org/docs/events.html) 이다
    - Synthetic events is a cross-browser wrapper around the browser's native event.
    - events work identically across all browsers
- JSX 콜백에서 this란.. 
    - JS 클래스 메소드들은 기본적으로 서로 [bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind) 되어 있지 않다.
    - .bind(this) 를 하지 않으면 this 는 undefined로 인식된다.
    - 기본적으로 JS 에서는, 메소드를 참조하면서 methodName 끝에 ()를 붙이지 않고 {this.methodName} 처럼 호출하면, 해당 메소드를 bind를 반드시 해줘야 한다.
- bind 가 귀찮다면, arrow function을 이용한 public class fields syntax 를 사용하기를 추천한다. 
    - "결과적으로 화살표 함수를 사용하면 this의 유효 범위가 화살표 함수를 실행한 함수 내부로 변경된다. 달리 말하면 비동기 처리를 위해 새롭게 생성된 실행 컨텍스트의 전역 유효범위가 아닌 화살표 함수를 호출한 함수의 컨텍스트로 남아있게 된다." [출처: es6 스터디 모음 북](https://joshua1988.gitbooks.io/es6-study/arrow-function.html)

```js
handleClick = () => {
    console.log("this is ", this);
}

```

### 2. Passing Arguments to Event Handlers

- e 이외에 추가 인자를 이벤트 핸들러에 전달하는 경우는 흔하다. 
- arrow 함수를 사용한다면 명시적으로 e를 표기한다.
- bind 를 사용한다면, 추가 인자 값 외의 인자들은 자동으로 전달된다.

```js
<button onClick={(e)=> this.deleteRow(id, e)}>Delete Arrow</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Bind</button>
```