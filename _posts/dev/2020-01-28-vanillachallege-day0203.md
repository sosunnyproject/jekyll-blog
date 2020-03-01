---
layout: post
categories: dev
title: "바닐라 JS 챌린지 day02 day03"
date: 2019-01-28T13:01:27-05:00
last_modified_at: 2019-01-28T13:01:27-05:00
share: true
---

## DAY 2: 1.6 ~ 1.10 강의

### 1.6 your first JS variable 변수

- every line is an expression.
- expression on JS is an instruction

- order of variable creation?
  - create -> initialize -> use
  - create & initialize -> use


- primitive data types of JS
  - number
  - float
  - string
  - boolean


- how to organize the data
  - array: list of data
  - object: save data in a key-value type


## DAY 3: 2.1 ~ 2.4 강의

### Change Text by Mouse Actions

- addEventListener
- const superEventHandler 안에 function handlers 다 집어넣기
- 참고 링크: https://developer.mozilla.org/ko/docs/Web/Events
- boilerplate template: https://codesandbox.io/s/day-three-blueprint-dogw9

1차
``` js
const superEventHandler = (e) => {
  console.log(e.type);
  let eventType = e.type;
  if (eventType === "mouseover") {
    textTitle.innerHTML = "The mouse is here";
    textTitle.style.color = colors[0];
  } else if (eventType === "mouseleave") {
    textTitle.innerHTML = "The mouse just left";
    textTitle.style.color = colors[1];
  } else if (eventType === "resize") {
    textTitle.innerHTML = "You just resized the window";
    textTitle.style.color = colors[2];
  } else if (eventType === "contextmenu") {
    textTitle.innerHTML = "You just RIGHT clicked";
    textTitle.style.color = colors[3];
  }
};

```

2차
```js
const superEventHandler = {
  mOver: () => {
    textTitle.innerHTML = "The mouse is here";
    textTitle.style.color = colors[4];
  },
  mLeave: () => {
    textTitle.innerHTML = "The mouse just left";
    textTitle.style.color = colors[1];
  },
  wResize: () => {
    textTitle.innerHTML = "You just resized the window";
    textTitle.style.color = colors[2];
  },
  rightClick: () => {
    textTitle.innerHTML = "You just RIGHT clicked";
    textTitle.style.color = colors[3];
  }
};

//call event handlers

textTitle.addEventListener("mouseover", superEventHandler.mOver);
textTitle.addEventListener("mouseleave", superEventHandler.mLeave);
window.addEventListener("resize", superEventHandler.wResize);
window.addEventListener("contextmenu", superEventHandler.rightClick);

```
