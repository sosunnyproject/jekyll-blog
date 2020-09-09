---
layout: post
categories: dev
title: "css grid 그리드로 masonry 효과 내기"
date: 2020-09-08-T14:01:27-05:00
last_modified_at: 2020-09-08-T14:01:27-05:00
share: false
---


코드펜: https://codepen.io/sosunny/pen/QWNQzeN?editors=1100

```html
<div class='container'>
   <section class="grid-left-top item">a</section>
  
  <div class='grid-right-wrap item'>
      <section>e</section>
      <section>f</section>
      <section>g</section>
  </div>
  
  <div class="grid-left-bottom">
     <section class="item">b</section>
     <section class="item">c</section>
     <section class="item">d</section>
      <section class="item">a</section>
      <section class="item">a</section>
  </div>
```

```css
.container{
  display: grid;
  grid-template-columns: 1fr 1fr;
  
  display: -ms-grid;
  -ms-grid-columns: 1fr 10px 1fr;
  -webkit-column-gap: 10px;
  -moz-column-gap: 10px;
  
  column-gap: 10px;
}

.grid-left-top{
  grid-column-start: 1;
  grid-row-start: 1;
}

.grid-right-wrap{
  grid-row-start: 1;
  grid-row-end: 4;
}

.grid-left-bottom {
  grid-row-start: 2;  
}

.item{
  border: 1px solid red;
}
```