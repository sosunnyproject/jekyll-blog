## 2.1 ~ 2.4 강의

## 코드 챌린지

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
