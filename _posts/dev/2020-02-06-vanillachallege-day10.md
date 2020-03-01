---
layout: post
categories: dev
title: "바닐라 JS 챌린지 day10"
date: 2019-02-06T13:01:27-05:00
last_modified_at: 2019-02-06T13:01:27-05:00
share: true
---


## 3.# 강의 리뷰

### Random Number Generator

- [code solution](https://codesandbox.io/s/day-ten-solution-fnylk)
- [my code](https://codesandbox.io/s/empty-blueprint-g22zg)

#### Review
- 기능 구현 자체는 어렵지 않음
- p5 instance 생성해서 겹쳐볼까 시도하는 중

```html
<head>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/0.10.2/p5.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/0.10.2/addons/p5.sound.min.js"></script>
</head>
<body>
  <div id="sketch-holder"></div>
</body>
```

```js
// example
import * as p from "p5";

// ref my previous code: https://github.com/PoseNet-Interaction/posenet-demos/blob/master/sketch1.js#L21
var sketch = function(p) {
  let canvas;
  p.setup = function() {
    canvas = p.createCanvas(100, 100).parent("sketch-holder");
    p.background("rgba(0,0,0, 0.5)");
    canvas.position(0, 0);
    canvas.style("z-index", "-1");
  };

  p.draw = function() {
    p.background(100, 100, 100);
  };
};

var myp5 = new p5(sketch, document.getElementById("sketch-holder"));

```
