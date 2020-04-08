---
layout: post
categories: dev
title: "REACT JS 공식 문서 파헤치기 (2)"
date: 2020-03-22T14:01:27-05:00
last_modified_at: 2020-03-22T14:01:27-05:00
share: false
---

**리액트 공식 문서 복기**
- [Chapter2~3](2020-03-22-reactOfficialDoc1.md)
- [Chapter4~5](2020-03-22-reactOfficialDoc2.md)
- [Chapter6~7](2020-03-24-reactOfficialDoc3.md)
- [Chapter8~9](2020-03-25-reactOfficialDoc4.md)
- [Chapter10~11](2020-04-04-reactOfficialDoc5.md)

***

### **목표: 리액트 공식문서를 120% 활용할 수 있게끔 익숙해지기**
- https://reactjs.org/docs/hello-world.html
- https://reactjs.org/tutorial/tutorial.html 

## Chapter 4: [Components and Props](https://reactjs.org/docs/components-and-props.html)

### 1. Function and Class Components
- 자바스크립트 함수를 써서 컴포넌트를 간단하게 정의할 수 있다.
- 이 함수는 data를 가진 하나의 'props'(properties 속성의 줄임말) 객체 인자를 받고, 리액트 엘리먼트를 리턴한다.

```js
// 함수형
function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
}

// es6 클래스형
class Welcome extends React.Component{
    render() {
        return <h1>Hello, {this.props.name}</h1>;
    }
}
```

### 2. Rendering a Component

- DOM 태그만 있는 엘리먼트가 아니라, 사용자 정의 컴포넌트로도 나타낼 수 있다. 
- 사용자 정의 컴포넌트로 작성한 엘리먼트가 발견되면, JSX 어트리뷰트와 그 자식들을, 단일 객체로, 이 컴포넌트에 전달한다. 이 객체가 props이다. 
- 사용자 정의 컴포넌트 이름은 [대문자로 시작하라](https://ko.reactjs.org/docs/jsx-in-depth.html#user-defined-components-must-be-capitalized)
    - 엘리먼트가 소문자로 시작하는 경우는 `<div>` 같은 내장 컴포넌트라는 의미로 이해된다. 대문자로 해야지, js 파일 내에 사용자가 정의했거나 import한 컴포넌트를 가리킨다.

```js
// call 3
function Welcome(props) {
    return <h1> Hello, {props.name} </h1> 
}
// props.name과 아래 name: attribute 명칭이 같아야 한다.

// call 2
const element = <Welcome name="Sara" />;   

// call 1
ReactDOM.render(
    element,   
    document.getElementById('root')  
)
```

### 3. Composing Components
- 컴포넌트는 리턴 값에 다른 컴포넌트들을 refer 참조할 수 있다. 
    - 어느 depth level에서든지 추상 컴포넌트(same component abstraction)를 사용할 수 있다는 의미이다. 

### 4. Extracting Components 
 > 컴포넌트를 작은 단위로 쪼개는 것은 굳.

```js
function Avatar(props) {
    return ( 
        <img 
            src={props.author.avatarUrl}
            alt={props.author.name} 
        />
    )
}

function Comment(props){
    return (
        <div>
            <Avatar user={props.author} />
            {props.author.name}
            {props.text}
            {formatDate(props.date)}
        </div>
    )
}

const comment = {
    date: new Date(),
    text: "learning react",
    author : {
        name: "useruser",
        avatarUrl: "sdfsd"
    }
}

ReactDOM.render(
    <Comment 
        date={comment.date}
        text={comment.text}
        author={comment.author}
    />,
    document.getElementById('root');
)
```

### 5. Props are Read-only
- 함수나 클래스 컴포넌트 모두 자체 props를 수정할 수 없다. 리액트 컴포넌트는 props를 다룰 때 무조건 pure functions 처럼 동작해야 한다.
    - pure: 같은 인풋에는 같은 아웃풋을 항상 리턴해야 한다.
    - impure: 인풋으로 들어온 값을 변형시키는 경우


---

## Chapter 5: State and Lifecycle

### State
- props를 이용해서 Clock component를 encapsulate & reuse component로 만들 수 있다.
- 하지만 Clock 에 계속 새로운 인풋을 전달해서 타이머를 업데이트 시키는 게 아니라, Clock이 스스로 업데이트 하도록 만드는 것이 이상적이다.
    - 이것을 위해 state 를 사용한다.
- state: props와 유사하지만, private & 컴포넌트에 의해 fully controlled 된다

### 1. Converting a Function to a Class

1. React.Component를 확장하는 ES6 class 생성
2. render() 빈 메소드 추가
3. 함수 내용을 render() 안으로
4. props => this.props 로 변환 (render() 내부에서 )
5. 빈 함수 선언은 삭제

```js
class Clock extends React.Component {
    render() {
        return (
            <div>
                <h1>It is {this.props.date.toLocaleTimeString()}
                </h1>
            </div>
        )
    }
}
```

- render() 함수는 업데이트가 발생될 때마다 호출된다.하지만 같은 DOM노드로 <Clock />를 렌더링한다면, Clock 클래스의 인스턴스는 한개만 사용된다. 
    - 이는 local state, lifecycle 메소드를 사용할 수 있게 해준다.

### 3. Adding Local State to a Class
- date 를 props => state 로 옮기기

1. render() 메소드 내부: `this.props.date` => `this.state.date` 
2. `this.state`의 초기값을 부여하는 class constructor 생성자를 추가한다.
    - 클래스 컴포넌트는 항상 props로 기본 constructor를 호출해야 한다.
3. `<Clock />` 엘레먼트 에서 date prop은 삭제한다.

> 단, 지금 이 상태에서는 tick/timer 업데이트가 이루어지지 않는다

```js
class Clock extends React.Component {
    constructor(props) {
        super(props);
        this.state = {date: new Date()};
    }

    render() {
        return (
            <div>
            <h1>{this.state.date.toLocaleTimeString()}</h1>
            </div>
        )
    }
}
ReactDOM.render(
  <Clock />,  
  // instead of <Clock date={new Date()} />,
  document.getElementById('root')
);
```

### 4. Adding Lifecycle methods to a Class

- MOUNTING: Clock 엘리먼트가 DOM에 처음 렌더링 되는 때
- UNMOUNTING: Clock 에 의해 생성된 DOM 이 제거됐을 때

#### 실행 순서

1. ReactDOM.render() 에 `<Clock />` 이 전달된다. 리액트가 Clock component의 생성자를 호출한다. 생성자에서 `this.state` 가 초기 생성된다. 이 state는 나중에 업데이트 된다.
2. Clock 컴포넌트의 render() 메소드를 호출한다. 이 때, 리액트는 화면에 무엇을 출력할지 알게 된다. 리액트는 Clock의 렌더링 결과값에 맞춰 DOM을 업데이트 한다.
3. Clock 결과값이 DOM에 삽입되고, React 는 componentDidMount 라이프사이클 메소드를 호출한다. Clock 컴포넌트는 컴포넌트의 tick 메소드를 1초에 1번 호출하기 위해 브라우저에게 타이머를 만들도록 한다.
4. 브라우저는 매초에 tick 메소드를 호출한다. 그 내부에서는, Clock 컴포넌트가 setState()에 현재 시간이 담긴 객체를 호출하면서 UI를 업데이트 한다. setState() 호출 덕분에 리액트는 state가 바뀐 것을 감지하고, render() 메소드를 다시 호출해서 화면에 반영한다. 이번에는, render() 메소드의 this.state.date가 달라져서 렌더링 아웃풋에는 업데이트된 시간이 반영된다. 따라서 리액트는 DOM을 업데이트 한다.
5. Clock 컴포넌트가 DOM 에서 제거되는 경우가 있다면, Unmount 메소드가 호출되어서 timer 또한 멈추게 된다.

```js
import React from 'react';

class Clock extends React.Component {
    constructor(props) { ... }
    componentDidMount() { 
        // 컴포넌트 아웃풋이 DOM에 렌더링 된 이후에 실행
        // set up a timer
        this.timerID = setInterval(
            () => this.tick(), 1000
        );
    }  
    componentWillUnmount() {
        clearInterval(this.timerID)
     } 
     tick() {
         this.setState({
             date: new Date()
         });
     }
    render() { ... }
}
```

### 5. Using State Correctly

- **setState()에 대해서 알아야 할 3가지**

1. State를 직접 바꾸지 말것. 반드시 setState() 메소드를 이용할 것. 오직 생성자에서만 this.state에 바로 값을 assign 할 수 있다.

2. State 업데이트는 비동기적일 수 있다. 
    - 리액트 성능을 위헤 여러 setState() 호출이 하나의 업데이트에 한꺼번에 처리될 수도 있다..
    - this.props, this.state가 비동기적으로 업데이트될 수 있기 때문에 다음 state 를 계산할 때 이 값들에 의존해서는 안된다. 

    ```js
    // wrong: setState()가 object를 전달받아서 처리하는 경우
    this.setState({ counter: this.state.counter + this.props.increment})

    // right: setState()가 function을 인자로 받는 경우
    this.setState(function(state, props) {
        return counter: state.counter + props.increment;
    })
    ```

3. State 업데이트는 병합 merge 된다

    - setState()가 호출되면, 리액트는 현재 state를 하나의 객체로 병합한다. state 안에 여러 엘리먼트가 있고, 한 번에 하나만 업데이트 되더라도, 그 때마다 state 전부를 하나의 객체로 병합한다.

### 6. Date Flows Down

부모든 자식이든 어떤 컴포넌트도 특정 컴포넌트가 stateful, stateless 인지 알지 못한다. 그리고 컴포넌트가 함수형이든 클래스형이든 상관이 없어야 한다.

> 그렇기 때문에 state이 local, encapsulated 라고 표현된다. 자체 컴포넌트 외에는 어느 컴포넌트에서도 접근할 수가 없다.

컴포넌트는 자신의 state를 자식 컴포넌트에게 props로 넘겨줄 수도 있다. 사용자 정의 컴포넌트의 경우도 적용된다. 인자를 넘겨받는 컴포넌트는 해당 인자가 부모 컴포넌트의 state이었는지 props였는지 알지 못한다. 

> 이는 top-down / unidirectional 데이터 흐름이라고 불린다. 

모든 state는 어느 특정 컴포넌트에 소유되어 있고, 그 state로부터 나온 모든 data나 UI는 해당 컴포넌트 (트리 구조 상) '밑 below'에 있는 컴포넌트들에만 영향을 끼칠 수 있다. 

> 즉, flow down 하고, flow up은 할 수 없다는 이야기.
