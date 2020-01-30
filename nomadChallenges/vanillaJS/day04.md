## Vanilla JS Day 4

### if/else 사용하는 code challenge

- [window속성](https://developer.mozilla.org/en-US/docs/Web/API/Window)
- querySelector: #id, .class, normalTag 헷갈리지 말기
- document.bgColor 기본제공 API로 색깔 변경 가능
- resize 할 때마다 변경되게 하려면, function handler 붙여서 그 function 안에서 기능 구현
- [my sandbox code solution](https://codesandbox.io/s/empty-blueprint-9yfn0)

```js
const colors = ["#CD61FF", "#E87C61", "#FFDF78", "#82E861", "#6BF5FF"]; // adobe colors 에서 팔레트 가져옴.
let sizeText = document.querySelector("#sizeInfo");
document.bgColor = colors[0];

// https://developer.mozilla.org/en-US/docs/Web/API/Document/bgColor
const changeWindowColor = () => {
  const innerWidth = window.innerWidth;
  sizeText.innerHTML = "current window size is " + innerWidth;
  if (innerWidth < 300) {
    document.bgColor = colors[0];
  } else if (innerWidth < 600 && innerWidth > 300) {
    document.bgColor = colors[1];
  } else if (innerWidth < 900 && innerWidth > 500) {
    document.bgColor = colors[2];
  } else if (innerWidth < 1200 && innerWidth > 900) {
    document.bgColor = colors[3];
  } else {
    document.bgColor = colors[4];
  }
};

window.addEventListener("resize", changeWindowColor);
```
