---
layout: post
categories: dev
title: "REACT JS 공식 문서 파헤치기 (3)"
date: 2020-03-24T14:01:27-05:00
last_modified_at: 2020-03-24T14:01:27-05:00
share: false
---

## [Chapter 8. Lists and Keys](https://reactjs.org/docs/lists-and-keys.html)

- 자바스크립트에서 리스트를 변형하는 방식을 우선 알아보자
    - map() 함수를 사용한다. 
- 리액트에서 array를 list of elements로 변형하는 방식도 자바스크립트와 비슷하다.

### Rendering Multiple Components

- Build collections of elements => Include them in JSX using curly braces {}

```js
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map( (number) => <li>{number}</li> );

ReactDOM.render(
    <ul>{listItems}</ul>,
    document.getElementById('root');
)
```

### Basic List Component

- 보통 component 안에 리스트를 렌더링한다.
- 이전 예제를 => array of numbers 를 받고 list of elements를 리턴하는 컴포넌트로 리팩토링해보자
- 'key' 가 필요하다는 경고문이 뜰 것이다. list of elements 를 만들 때 포함되는 특수한 문자열 attribute 이다. 왜 중요한지는 하단에서...

```js
    function NumberList(props){
        const numbers = props.numbers;
        const listItems = numbers.map( (number) =>
            <li>{number}</li>
        ) 
        return(
            <ul>{listItems}</ul>
        )
    }
    const numbers = [1, 2, 3, 4, 5];

    ReactDOM.render(
        <NumberList numbers={numbers} />,
    document.getElementById('root');
)
```


### Keys

- 어떤 아이템이 변경, 추가, 제거되었는지 리액트가 알기 쉽도록 해준다. 
- 엘리먼트에 고정된 identity를 주기 위해서 array 안의 엘리먼트에 키 값을 부여해준다.
- 유일한 id 값 혹은 item index 를 보통 사용한다.

```js
const listItems = numbers.map( (n) => 
    <li key={n.toString()}>{n}</li>
    )

const todoItems = todos.map( (todo) => 
    <li key={todo.id}> {todo} </li>
)

// Not Recommended if the order of items may change
const todoItems = todos.map( (todo, index) => 
    <li key={index}> {todo.text} </li>
)
```

### Extracting Components with Keys

- Key 는 주변 array의 context 에서만 의미가 있다.
- ListItem 컴포넌트를 추출한다면, ListItem 안의 li 가 아니라, ListItem 엘리멘트 (in the array) 가 key를 가져야 한다.
- 즉, ListItem를 호출/생성하는 부분에서 key가 부여되어야 한다.
- [예시 코드](https://codepen.io/gaearon/pen/ZXeOGM?editors=0010)

### Keys must only be unique among siblings

- 같은 엘리먼트 내부에서는 유니크한 값이어야 하지만, 글로벌하게 유일할 필요는 없다.
- 같은 아이템을 지칭한다면, 해당 키를 여러 컴포넌트에서 사용할 수 있다.
- 컴포넌트에서 props.key 로 key 값을 읽을 수 없다.

### Embedding map() in JSX

- curly braces {} 안에 map() 을 넣어서 embedding expression 할 수 있다.
- 위의 NumberList 함수를 이렇게 바꿀 수 있다.

```js
 function NumberList(props){
        const numbers = props.numbers;

        return(
            <ul>
                {numbers.map( (number) =>
                <ListItem key={number.toString()}
                    value={number} />
                )}
            </ul>
        )
    }
```