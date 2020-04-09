---
layout: post
categories: dev
title: "REACT JS 심화 살펴보기"
date: 2020-03-22T14:01:27-05:00
last_modified_at: 2020-03-22T14:01:27-05:00
share: false
---

1. 최적화
[Optimizing Performance](https://reactjs.org/docs/optimizing-performance.html#avoid-reconciliation)

2. React memo
- props가 부분적으로 변경되어도, 변경되지 않은 컴포넌트들은 re-rendering 하지 않게 하는 기법
[React memo](https://reactjs.org/docs/react-api.html#reactmemo)

3. Spread
- 위와 같이 react memeo를 썻을 때, array, object 같은 애들은 주소값이 변경되어야지 re-rendering을 한다. 
- array 에 엘리먼트를 그냥 추가로 push 하는게 아니라, spread syntax 를 활용해야지 array object가 업데이트 된다. 
- [es6 spread](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)