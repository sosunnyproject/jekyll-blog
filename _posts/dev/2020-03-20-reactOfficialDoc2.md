---
layout: post
categories: dev
title: " REACT JS 공식 문서 파헤치기 (2)"
date: 2020-03-22T14:01:27-05:00
last_modified_at: 2020-03-22T14:01:27-05:00
share: false
---

### **목표: 공식문서를 120% 활용할 수 있게끔 익숙해지기**
- https://reactjs.org/docs/hello-world.html
- https://reactjs.org/tutorial/tutorial.html 

## [Rendering Elements](https://reactjs.org/docs/rendering-elements.html)

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
function tick() {
    const element =  <div> ... </div>;
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

