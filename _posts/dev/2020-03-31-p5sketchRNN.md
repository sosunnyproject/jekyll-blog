---
layout: post
categories: creativecoding
title: "P5 x SketchRNN"
date: 2020-03-31T14:01:27-05:00
last_modified_at: 2020-03-31T14:01:27-05:00
share: false
---

1. index.html 에 src 추가하기
- [Your index.html](https://learn.ml5js.org/docs/#/tutorials/hello-ml5?id=code)

```html
<html>
<head>
  <meta charset="UTF-8">
  <script src="https://unpkg.com/ml5@0.4.3/dist/ml5.min.js"></script>
  <!-- p5 script src -->
</head>
<body></body>
</html>
```

2. QuickStart

- 모델을 preload하기 때문에 callback 파라미터는 필요 없다.
- models 변수 대신에 특정 스트링 배열로 어떤 모델을 호출할지 정한다. 
    - [available models](https://github.com/ml5js/ml5-library/blob/master/src/SketchRNN/models.js)

```js
let sketchRNN;

function preload(){
  sketchRNN = ml5.sketchRNN('cat'); 
}

function setup() {
  createCanvas(400, 400);
  console.log('model loaded');
}

function draw() {
  background(220);
}
```

3. gotStrokePath() 메소드

- 코드

```js
// 글로벌에 추가
function gotStrokePath(error, strokePath) {
   console.log(strokePath); 
}
```

- 결과값

```json
Object {dx: -7.009424007547129, dy: -2.5481305925730413, pen: "down"}
dx: -7.009424007547129
dy: -2.5481305925730413
pen: "down"
```

4. initial stroke, many strokes

```js
let sketchRNN;
let currentStroke;
let x, y;

// preload function

function setup() {
  createCanvas(400, 400);
  sketchRNN.generate(gotStrokePath);
  x = width/2;
  y = height/2;
  console.log('model loaded');
}

// gotStrokePath function

function draw() {
  background(220);
  
  if (currentStroke) {
    stroke(0);
    strokeWeight(4);
    // 1. initial stroke
    line(x, y, x+ currentStroke.dx, y + currentStroke.dy); 

    // 3. start currentStroke at latest point
    x += currentStroke.dx;
    y += currentStroke.dy;

    // 2. stroke loop
    currentStroke=null;
    sketchRNN.generate(gotStrokePath);
  }
}
```
