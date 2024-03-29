---
layout: post
categories: dev
title: "바닐라 JS 챌린지 day0708"
date: 2019-02-03T13:01:27-05:00
last_modified_at: 2019-02-03T13:01:27-05:00
share: false
---


## 3.3 ~ 3.7 강의

### ToDoList with Events, localStorage

- [submit code sandbox link](https://codesandbox.io/s/empty-blueprint-c2guw)
- [code solution](https://codesandbox.io/s/day-eight-nine-solution-8817f)

```
Make a To Do list with two boards: Pending, Finished.
Allow the user to switch between boards.
Allow the user to delete To Dos.
Save everything on localStorage and restore everything on refresh.
```

### 3.5 강의
- `<form><input>` 태그: 입력창, 입력값
- `<ul><li>` 태그: 리스트 값 
- `<li>` 값 생성: `document.createElement, li.appendChild` 메소드 사용해서 flexible 하게 각 리스트별 텍스트 및 버튼 생성
- localStorage : pending, finished 두 개 만들기

### 3.6 강의
- todos 를 array object 로...


### Major Debug

1. array 에 담긴 object의 id 값을 access 하려고 하는데, console에서 object는 찍히지만, property 값이 undefined 로 나옴. 
- 다른 함수 안에서는 잘 실행되는 것을 확인
- 아마 시간차의 문제인 듯 해서, if 조건문을 사용해서 undefined 인 경우를 제외하도록 디버깅
- array's last item's id 값을 구하는 이유: if not, 기존 array 에 담긴 object의 id 와 충돌하는 경우가 발생해서, 삭제하거나 할 때 에러 발생함. id 값이 겹치지 않도록 조치.
```
// paint finished list
function createFinished(todo) {
  // create li with btn
  let newId = finishedTodos.length + 1;
  if (finishedTodos.length !== 0) {
    const lastItem = finishedTodos[finishedTodos.length - 1];
    newId = lastItem.id + 1;
    console.log(newId);
    // if 문 체크 안하는 경우, 로딩이 미처 안되어서 property access 를 못함.
  }
  const li = document.createElement("li");

// 이하 생략
```

2. parseInt 파라미터 실수
- 두번째 인자는 n진수를 결정하는데, 2라고 써서 계속 오류 났었음
```
  // delete according index
  const cleanTodos = toDos.filter(function(todo) {
    return todo.id !== parseInt(li.id, 10);
  });
```

3. 코드 divide 해보기

- li 태그를 그리는 부분들 중 겹치는 게 있음.
- 기존 방식: createPending(), createFinished() 각각에서 li 태그 및 하위 속성들을 다 그린다.
```js
// paint pending list
function createPending(todo) {
  // create li with btn
  const li = document.createElement("li");
  let newId = pendingTodos.length + 1;
  if (pendingTodos.length !== 0) {
    const lastItem = pendingTodos[pendingTodos.length - 1];
    newId = lastItem.id + 1;
  }
  const doneBtn = document.createElement("button");
  const delBtn = document.createElement("button");
  const textTodo = document.createTextNode(todo);
  doneBtn.innerText = "🙆‍♀️";
  delBtn.innerText = "🙅";
  li.id = newId;
  li.appendChild(doneBtn);
  li.appendChild(delBtn);
  li.appendChild(textTodo);
  pending.appendChild(li);

  // addEventListener: action per button
  delBtn.addEventListener("click", deleteTodo);
  doneBtn.addEventListener("click", moveTodo);

  // save as an object, not string
  const todoObj = { content: todo, id: newId };
  pendingTodos.push(todoObj);
  saveToPending(); // save the updated array
}
```
- 분할 후 코드
  - .insertBefore 이라는 메소드를 써서 pending/finished 각각 다른 버튼을 따로 li 태그 안에 추가해야함.

```js
function buildGenericLi(todo, todoList) {
  // create li with btn
  let newId = todoList.length + 1;
  if (todoList.length !== 0) {
    const lastItem = todoList[todoList.length - 1];
    newId = lastItem.id + 1;
    console.log(newId);
    // if 문 체크 안하는 경우, 로딩이 미처 안되어서 property access 를 못함.
  }
  const li = document.createElement("li");
  const delBtn = document.createElement("button"); // delete
  const textTodo = document.createTextNode(todo);
  delBtn.innerText = "🙅";
  li.id = newId;
  li.appendChild(delBtn);
  li.appendChild(textTodo);
  todoList.appendChild(li); // add to html
  return li;
}

// paint finished list
function createFinished(todo) {
  const li = buildGenericLi(todo, finishedTodos);
  const delBtn = li.childNodes[0];
  console.log(delBtn);

  const backBtn = document.createElement("button"); // back to Pending
  backBtn.innerText = "🤷";
  li.insertBefore(backBtn, delBtn);

  // addEventListener: action per button
  backBtn.addEventListener("click", backToPending);
  delBtn.addEventListener("click", deleteTodo);

  // save as an object, not string
  const doneObj = { content: todo, id: li.id };
  finishedTodos.push(doneObj);
  saveToFinished(); // save current [] to localStorage
}
```

- parameter 입력 값으로 pending/finished를 구별해서 createPending/createFinished를 더욱 줄여보기
```js

// create li with btn
function buildGenericLi(todo, parentList, parentName) {
  let newId = parentList.length + 1;
  if (parentList.length !== 0) {
    const lastItem = parentList[parentList.length - 1];
    newId = lastItem.id + 1;
    console.log(newId);
    // if 문 체크 안하는 경우, 로딩이 미처 안되어서 property access 를 못함.
  }
  const li = document.createElement("li");
  const textTodo = document.createTextNode(todo);
  const delBtn = document.createElement("button"); // delete
  li.id = newId;
  delBtn.innerText = "🙅";
  li.appendChild(delBtn);
  li.appendChild(textTodo);
  delBtn.addEventListener("click", deleteTodo);

  let extraBtn;
  if (parentName === "pending") {
    extraBtn = document.createElement("button");
    extraBtn.innerText = "🙆‍♀️";
    extraBtn.addEventListener("click", moveTodo);
  } else {
    extraBtn = document.createElement("button"); // back to Pending
    extraBtn.innerText = "🤷";
    extraBtn.addEventListener("click", backToPending);
  }

  li.insertBefore(extraBtn, delBtn);
  return li;
}

// paint pending list
function createPending(todo) {
  const li = buildGenericLi(todo, pendingTodos, "pending");
  pending.appendChild(li); // add to html tag

  // save as an object, not string
  const todoObj = { content: todo, id: parseInt(li.id) };
  pendingTodos.push(todoObj);
  saveToPending(); // save current [] to localStorage
}

// paint finished list
function createFinished(todo) {
  const li = buildGenericLi(todo, finishedTodos, "finished");
  finished.appendChild(li); // add to html tag

  // save as an object, not string
  const doneObj = { content: todo, id: parseInt(li.id) };
  finishedTodos.push(doneObj);
  saveToFinished(); // save current [] to localStorage
}
```