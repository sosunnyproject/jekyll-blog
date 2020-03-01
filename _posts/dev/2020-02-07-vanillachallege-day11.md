---
layout: post
categories: dev
title: "바닐라 JS 챌린지 day11"
date: 2019-02-07T13:01:27-05:00
last_modified_at: 2019-02-07T13:01:27-05:00
share: false
---

## Review

### Calculator 만들기

- [my code](https://codesandbox.io/s/empty-blueprint-fwl3g)
- [solution code](https://codesandbox.io/s/day-11-12-solution-mwmoi)
- [my second code](https://codesandbox.io/s/lucid-thompson-p8tm7)

1. 버그: - 값을 계속 눌렀을 때, 음수로 계산할지 아닌지 판단해야함
    - 두번째 코드에서 subtractClicked 변수로 홀수/짝수인지 구별함
    - subtractClicked 를 언제 0, 1 로 초기화할지 고민하는 게 관건이었음
```js
let subtractClicked = 0;

// operation - switch
function executeOperation() {
  const intA = parseInt(firstVal, 10);
  const intB = parseInt(secondVal, 10);
  switch (currentOp) {
    case "+":
      return intA + intB;
    case "/":
      return intA / intB;
    case "*":
      return intA * intB;
    case "-":
      if (subtractClicked % 2 === 1) {
        return intA - intB;
      } else {
        return intA + intB;
      }
    default:
      return;
  }
}
// 중간 생략


function handleOpClick(e) {
  if (firstVal.length !== 0 && secondVal.length !== 0) {
    // if first, second values are not empty, calculate;
    calculate();
    currentOp = e.target.textContent;
    if (currentOp === "-") {
      subtractClicked = 1; // start from 1
    } else {
      subtractClicked = 0;
    }
  } else {
    currentOp = e.target.textContent;
    if (currentOp === "-") {
      subtractClicked += 1; // start from 1
    }
  }
  record(currentOp);
}

function handleClear() {
  currentOp = "";
  secondVal = "";
  firstVal = "";
  subtractClicked = 0;
  input.innerHTML = "0";
  records = [];
  progress.innerHTML = "0";
}

function handleResult() {
  if (firstVal.length !== 0 && secondVal.length !== 0) {
    calculate();
    records = [];
    subtractClicked = 0;
    records.push(input.innerHTML);
    progress.innerHTML = records.join("");
  } else {
    return;
  }
}
```
