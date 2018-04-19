---
layout: default
---

*사내스터디 ES6 중 일부 노트정리입니다. 풀 노트는 https://joshua1988.gitbooks.io/es6-study/content/ 를 참조하세요.*

# Const / Let / Var

#### scoping: "where can these variables be accessed" 어디서부터 어디파트까지 이 변수를 사용할 수 있는가
- block-scoped: if { HERE  }, for() {   HERE  }....
- function-scoped: function() { HERE  }

#### hoisting? (es5...)
- Hoisting is JS's default behavior of moving all declarations to the *TOP* of the current scope (to the top of the current scirpt or the current function)
- JS only hoists declaration, not initialization.
- _??ES 6??_

불가능
```javascript
x = 5;
console.log(x);
const x=10;
```
가능
```javascript
x = 5;
console.log(x);
//let x; 가능
let x=10;
```


## ES 5 
1. var
- easy to have global and local variables collide
- function 안에서 선언하지 않았으면 globally scoped.
- 두 번 선언/정의 해도 에러가 안뜸


2. var & hoisting

- "Javascript: a variable can be declared after it has been used."
- "Because hoisting behavior of JS: moving all declaration to the top!"
- "JS only hoists declarations, not initializations."

> when i switch x = 5; <---> var x; in the code below, it returns 'undefined' because it cannot bring up initialization to the top.

```
<html> 
<body>
<p id="demo"></p>
<script>
x = 5;
elem  = document.getElementById("demo");
elem.innerHTML = x;
var x;
</script>
<body>
</html>
```

## ES 6

### const
- block-scoped
- cannot change the value, but doesn't mean it's _immutable_. 값을 바꿀 수는 없지만, immutable까지는 아니다.
- you can change the content of objects inside. (예, redux/react) 

### let
- block-scoped
- cannot re-declare. you can re-define. 같은 이름으로 새로운 선언을 할 수 없다. 다른 값으로 재정의는 가능하다.
- inner functions - useful

### var
- function-scoped
- can override. (this would cause error, especially when you forgot you already used that variable name)
- _??if wanna use like 'var' (es5 var), you have to create a different context using a closure to preserve the value??_
    - [mozilla example-code](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)



> ref: https://www.w3schools.com/js/js_hoisting.asp 

> ref: https://appendto.com/2016/12/when-to-use-es5-var-vs-es6-let-2/

> ref: https://www.youtube.com/watch?v=q8SHaDQdul0 

> ref: Udemy - https://www.udemy.com/react-2nd-edition/ 


# Arrow Function

```javascript
(arguments) => { 
    return _____ ;
}

// {} this is optional

(a,b) => return a+b;


function() {
    this.refersToThisFunction
}


() => {
    this.refersToClass
}
```

# Example codes for const/let/var, arrow function

## const,let,var in REACT
[code](https://github.com/poscoict-arvrmr/second/tree/master/app/reducers)
_redux - part of reducer code_

```javascript
const defaultState = {
    isConnected: true,   //wifi
    isSignedin: false,   //login
    isRecording : false  //camera
}
console.log(defaultState);
console.log("------------REDUCER/defaultState---------------");

export default function checker(state=defaultState, action){
    switch(action.type){
        case START_REC :
            console.log('[reducer/STARTREC]', 'reducer', state, action);
            return {
                ...state,
                isRecording:true
            }
        case STOP_REC :
            console.log('[reducer/STOPREC]', 'reducer', state, action);
            return {
                ...state,
                isRecording:false
            }
        default :
            return state;
    }
}
```



## Arrow in REACT
[code](https://github.com/sosunnyproject/react-test/tree/master/movie_app)
```javascript
class App extends Component {
//lifecycle events (e.g. componentWillMount) or set any state you should use class.
// const App = props => { return <Movie /> }; is possible if you want stateless, functional components
  render() {
    return (
      <div className="App">
        {movies.map((movie, index) => {
          return <Movie title={movie.title} poster={movie.poster} key={index} />
        })}
      </div>
    );
  }
}
```

```javascript
//ES5 function writing
    // setTimeout(function(){
    //   console.log('hello')
    // }, 1000)

setTimeout(() => console.log('hello'), 1000);
```

```javascript
//state = { movies:[ ] } defined.
setTimeout( () =>
    {
      this.setState(
        {
          movies: [
            //... brings-all-pre-defined-stuff
          ...this.state.movies,
           // new object you want to add to the movies array
          {
            title: "Chef's Table",
            poster:"https://upload.wikimedia.org/wikipedia/en/1/11/Chef%27s_Table.jpg"
          }
        ]
      })
    }, 1000);
  }
  ```
--------------------------------------------------------------------------------------------

# Object Literal

### Properties를 간단하게

**1. ES6: initialize properties with shorter syntax**
```
const basic = {name: 'susan', age: 24, location: {past: 'New York', current: 'Seoul'}};
console.log(basic.location.past);       // "New York"
const name = 'susan';
const age = 24;
const location = {past: 'New York', current: 'Seoul'};

const basic6= {name, age, location};
console.log(basic6.age);                // 24
console.log(basic6.location.current);   // "Seoul"
```

**1. ES5**
```js
const basic5= {name: name, age: age, location: location};
```

**2. ES6: Computed property names**
- 동적으로 property names 생성가능
- property accesor 처럼 [ ] notation 사용
- [] 안에서 computation 진행됨
```
const hobby = 'hobby';
const privacy = {
  [hobby]: 'climbing',
  ['birth' + 'day']: 'November'
};
```

**2. ES5**
```
var hobby = 'hobby';
var privacy = (_privacy = {}, 
_defineProperty(_privacy, hobby, 'climbing'), 
_defineProperty(_privacy, 'birth' + 'day', 'November'), _privacy);
console.log(privacy);

//console-prints below: both ES5 and ES6
console.log(privacy);   //  Object { hobby: "climbing", birthday: "November" }
console.log(privacy[hobby]);  // "climbing"
console.log(privacy.birthday);  // "November"

```

> reference: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer
> refernce: http://www.benmvp.com/learning-es6-enhanced-object-literals/
> https://ponyfoo.com/articles/es6-object-literal-features-in-depth
>

### Object.assign() OR Spread Properties in ES6
    - 더 짧은 문법으로 shallow-cloning (except prototype) or merging objects 가능.
    - 그 전에는 Object.assign(): setters 를 작동시킨다. spread operator 는 안 그럼.


**3. ES5: assign 함수를 사용한다.**
```js
const es5_one = { a: 1, b: 2, c: 3 };
const es5_two = { d: 1, e: 2, f: 3 };
const es5_merged = Object.assign({}, es5_obj);
// Object { a: 1, b: 2, c: 3, d: 1, e: 2, f: 3 }
```
**3. ES6: ... 으로 spread 기능 : 간단하게 표기 가능하다.**
```
const es6_one= { company:'Naver', location: 'Jeongja' }
const es6_two = { company: 'Kakao', location: 'Pangyo' }
const es6_three = {food: 'good', facility: 'good'}

// 합칠 때는 ... 을 붙여주자
const es6_clone = {...es6_one};
const es6_merged = {es6_one, es6_two};
// Object { es6_one: Object { company: "Naver", location: "Jeongja" }, es6_two: Object { company: "Kakao", location: "Pangyo" } }

// 같은 properties 이름이 있으면 마지막 아이로 override되버린다.
const es6_merged2 = {...es6_one, ...es6_two};
// Object { company: "Kakao", location: "Pangyo" }

// 보통, 정상적인 merge
const es6_merged3 = {...es6_one, ...es6_three};
// Object { company: "Naver", location: "Jeongja", food: "good", facility: "good" }
```
> spread properties: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax


# React 

### Structure of React 
1. [Structure a React App](https://hackernoon.com/the-100-correct-way-to-structure-a-react-app-or-why-theres-no-such-thing-3ede534ef1ed) (English)
2. [프로젝트의디렉토리구조](https://medium.com/@FourwingsY/react-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8%EC%9D%98-%EB%94%94%EB%A0%89%ED%86%A0%EB%A6%AC-%EA%B5%AC%EC%A1%B0-bb183c0a426e)(한국어)
3. [유용한설명링크모음](https://github.com/markerikson/react-redux-links/blob/master/react-architecture.md)(영어)
4. [Conceptually understanding React Component](https://ifelse.io/2016/10/20/a-conceptual-introduction-to-react-components/)(영어)

**요약**
- Divide and Conquer: [Atomic design approach](https://cdn-images-1.medium.com/max/1600/1*m2fb_YCpY3WUJxKNUjLPdA.png)
- [Easy Navigation](https://cdn-images-1.medium.com/max/2000/1*Pmm5N4hr9cANciDL5nbDpw.png) : Think how your computer navigates through your app and what would be easy for it 
- [React Component 해부 그림](https://cdn.ifelse.io/images/2.1.png)
- [Components are *composable*. They can have parent-child relationships](https://cdn.ifelse.io/images/2.6.png)

