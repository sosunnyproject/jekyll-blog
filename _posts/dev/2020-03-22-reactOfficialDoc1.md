---
layout: post
categories: dev
title: "REACT JS 공식 문서 파헤치기 (1)"
date: 2020-03-22T13:01:27-05:00
last_modified_at: 2020-03-22T13:01:27-05:00
share: false
---

### **목표: 리액트 공식문서를 120% 활용할 수 있게끔 익숙해지기**
- https://reactjs.org/docs/hello-world.html
- https://reactjs.org/tutorial/tutorial.html 

## Chapter 2: [Introducing JSX](https://reactjs.org/docs/introducing-jsx.html)

### 1. Why JSX?

- 자바스크립트를 확장한 문법: syntax extension of JS
- 컴포넌트: Loosely coupling markup and logic units into 'components' 

### 2. Embedding Expressions in JSX

```js
function formatName(user) {
    return user.firstName + ' ' + user.lastName;
}
const name = {
    firstName: 'Harper',
    lastName: 'React'
}
const element = <h1> Hello, {formatName(user)} </h1>;

ReactDOM.render(
    element,
    document.getElementById('root')
);
```

### 3. JSX Prevents Injection Attacks (주입 공격 방지)

- ReactDOM은 렌더링하기 전에 JSX에 삽입된 모든 value를 escape 한다. 모든 값은 렌더링 되기 이전에 스트링으로 변환된다. 이 특성은 XSS (cross-site-scripting) 공격을 방지해준다. 
- HTML [escape](https://stackoverflow.com/questions/7381974/which-characters-need-to-be-escaped-in-html) characters (필수): &amp , &lt, &gt, &quot, &#39 (&, <, >, ", ');
- [XSS: cross-site-scripting](https://en.wikipedia.org/wiki/Cross-site_scripting)
    - 웹 어플리케이션에서 발견되는 컴퓨터 보안 취약 특성 중의 하나
    - 다른 유저가 보고 있는 웹 페이지에 client-side 스크립트를 주입해서 공격한다.
    - same-origin policy 같은 액세스 컨트롤을 우회해서 해킹하는 수법에 취약하다.

### 4. JSX Represents Objects: 객체를 표현한다

- Babel은 React.createElement() 호출을 통해 JSX 를 컴파일한다
- React.createElement() 는 버그 없는 코드가 되도록 몇가지 검사를 수행한다. 
- 'React Elements' 라는 객체를 생성한다. 화면에 보이는 객체에 대한 설명이라고 볼 수 있다. 리액트는 이 객체를 읽고, DOM을 구성하는 데에 사용한다.

```js
const element = <h1 className="greeting"> Hello World</h1>;

// same as above
const element = React.createElement(
    'h1', {className: 'greeting'}, 'Hello World'
);

// above creates below object: React Elements
const element = {
    type: 'h1',
    props: {
        className: 'greeting',
        children: 'Hello World'
    }
};
```

---

## Chapter 3: [Rendering Elements](https://reactjs.org/docs/rendering-elements.html)

### 1. Rendering an Element into the DOM

- single root DOM node: `<div id="root"></div>`
    - div 안의 엘리먼트는 모두 REACT DOM 이 관리하게 된다.
- React element를 root DOM node 안에 렌더하기 위해서는 ReactDOM.render()로 둘 다 (element & root node) 전달한다.

```js
const element = <h1> Hello, World </h1>;
ReactDOM.render(element, document.getElementById('root'));
```

### 2. Updating the Rendered Element 

- 리액트 엘리먼트는 한 번 만들면 바꿀 수 없다. 
- 현재로서, 새로운 엘리먼트를 생성하기 위해 UI를 업데이트하는 방법은 새 엘리먼트를 ReactDOM.render()로 넘기는 것이다. 
    - ReactDOM.render()를 재호출하는 것.

```js
// clock component example 

function tick() {
    const element =  <div> <h1>{new Date().toLocaleTimeString()}. </h1> </div>;
    ReactDOM.render(element, document.getElementById('root'));
}
setInterval(tick, 1000);
```

### 3. React Only Updates What's Necessary: 리액트는 필수적인 것만 업데이트한다.

- ReactDOM은 해당 엘리먼트와 그 자식엘리먼트를, 이전 엘리먼트와 비교한 후, 필요한 경우에만 업데이트한다.
    - 위의 예시 코드에서, div 안에 
    ```html 
    <h1>Hello, world!</h1>
    <h2>It is {new Date().toLocaleTimeString()}.</h2> 
    ```
    여러 children이 있어도, 계속 변해야 하는 h2 엘리먼트만 업데이트 한다.

