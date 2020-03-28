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

## [Chapter 6 HandlingEvents](https://reactjs.org/docs/handling-events.html)

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
    - "결과적으로 화살표 함수를 사용하면 this의 유효 범위가 화살표 함수를 실행한 함수 내부로 변경된다. 달리 말하면 비동기 처리를 위해 새롭게 생성된 실행 컨텍스트의 전역 유효범위가 아닌 화살표 함수를 호출한 함수의 컨텍스트로 남아있게 된다." 
        - [출처: es6 스터디 모음 북](https://joshua1988.gitbooks.io/es6-study/arrow-function.html)

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

## [Chapter 7 Conditional Rendering](http://reactjs.org/docs/conditional-rendering.html)

- 원하는 동작을 encapsulate 캡슐화하는 컴포넌트를 만들 수 있습니다. 이렇게 하면 애플리케이션 상태에 따라 컴포넌트 중 몇 개만을 렌터링할 수 있다.
- 자바스크립트의 조건 처리와 비슷하게 동작한다. if와 같은 조건부 오퍼레이터로 현재 상태를 나타내는 엘리먼트를 생성하고, 리액트를 그에 맞게 UI를 업데이트하도록 한다.

```js
    function UserGreeting(props){
        return <h1>Welcome back!</h1>;
    }

    function GuestGreeting(props){
        return <h1>Please sign up</h1>;
    }

    function Greeting(props){
        const isLoggedIn = props.isLoggedIn;
        if (isLoggedIn) {
            return <UserGreeting />;
        } else {
            return <GuestGreeting />;
        }
    }

    ReactDOM.render(
        // Try Changing to isLoggedIn={true};
        <Greeting isLoggedIn={false} />,
        document.getElementById('root')
    );
```

### Element Variables  엘리먼트 변수

- 엘리먼트를 저장하기 위해 변수들을 사용할 수 있다. 컴포넌트의 특정 부분만 조건적으로 렌더링하면서 나머지 결과값은 그대로 둘 수 있다. 
- 아래 예시에서는 stateful component : LoginControl 를 생성할 것이다.

```js
function LoginButton(props){
  <button onClick={props.onClick}> Login </button>
}

function LogoutButton(props){
  <button onClick={props.onClick}> Logout </button>
}

class LoginControl extends React.Component {
    constructor(props){
        super(props);
        this.state = {isLoggedIn: false};
        this.handleLoginClick = this.handleLoginClick.bind(this); // this: LoginControl Component
        this.handleLogoutClick = this.handleLogoutClick.bind(this);
    }

    handleLoginClick(){
        this.setState({isLoggedIn: true});
    }

    handleLogoutClick(){
        this.setState({isLoggedIn: false});
    }

    render(){
        const isLoggedIn = this.state.isLoggedIn;
        let button;
        if (isLoggedIn) {
            button = <LogoutButton onClick={this.handleLogoutClick} />;
        } else {
            button = <LoginButton onClick={this.handleLoginClick} />;
        }

        return(
            <div>
                <Greeting isLoggedIn={this.state.isLoggedIn} />
                {button}
            </div>
        )
    }

     ReactDOM.render(
        <LoginControl  />,
        document.getElementById('root')
    );
}
```
### Inline If with Logical && Operator

- if 조건문 대신 더 짧은 문법으로 inline conditions in JSX 가 가능하다.
- curly braces 중가로 안에 [Embedding Expressions in JSX](https://ko.reactjs.org/docs/introducing-jsx.html#embedding-expressions-in-jsx) 사용하기 
- JS 로직 오퍼레이터 && 을 사용한다. 
    - true && expression => expression, false && expression => false 로 항상 리턴하기 때문이다.
    - 조건이 참이라면, && 바로 뒤의 엘리먼트가 리턴된다.    

```js
    //...
    return(
        <div>
            {this.state.isLoggedIn && 
                <h1> Welcome to ReactJS.ORG.</h1>
            }
        </div>
    )
```

### Inline If-Else with Conditional Operator 

- JS 조건부 오퍼레이터: `condition ? true: false`

```js
    return(
        <div> The user is <b>{isLoggedIn? 'currently' : 'not'}</b> logged in. </div>
    );
```

### Preventing Component from Rendering 

- 컴포넌트가 다른 컴포넌트에 의해 렌더링 되었지만, 숨기고 싶은 경우가 있다. 
    - 렌더링 아웃풋 대신 return null 을 해야 한다.
- [이 예시](https://codepen.io/gaearon/pen/Xjoqwm?editors=0010)에서는 WarningBanner 컴포넌트가 warn 이라는 prop 에 따라 렌더링된다. 
    - prop 값이 false 라면, 컴포넌트가 보이지 않는다. 