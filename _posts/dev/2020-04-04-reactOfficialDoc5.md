---
layout: post
categories: dev
title: "REACT JS 공식 문서 파헤치기 (3)"
date: 2020-03-24T14:01:27-05:00
last_modified_at: 2020-03-24T14:01:27-05:00
share: false
---

## [Chapter 10 State 끌어올리기](https://ko.reactjs.org/docs/lifting-state-up.html)

- 동일한 데이터에 대한 변경사항을 여러 컴포넌트에 반영해야 할 때
  - the closest common ancestor 로 state를 끌어올리기

### 예시 코드: 주어진 온도에서 물이 끓는 지의 여부 추정하는 온도 계산기
    
### 1. BoilingVerdict function 컴포넌트

  - 파라미터: celsius 라는 prop 받아서 이 온도가 물이 끓기에 충분한지 출력

### 2. Calculator Class 컴포넌트

  - render() : input 
  - input 태그의 value를 this.state.temperature 에 저장 & BoilingVerdict 에 파라미터로 전달
  - handleChange(e): setState()

### 3. Celsius & Fahrenheit 추가하기

  - `const scaleNames = {c: 'Celsius', f: 'Fahrenheit'} `
  - Calculator 내부 => TemperatureInput Class에 copy
    - render() 에 scale 추가
    
  ```js
    render(){
      const temp = this.state.temp;
      const scale = this.props.scale;
      return(
        <fieldset>
          <legend> Enter temp in {scaleNames[scale]}: </legend>
          <input value={temp} onChange={handleChange} />
        </fieldset>
      );
    }
  ```

### 4. Calculator 클래스 단순화
  
  - 문제점: celsius 칸과 fahrenheit 칸의 입력값이 동기화되지 않고, 따로 놈.

  ```js
    class Calculator extends React.Component{
      render(){
        return(
          <div>
            <TemperatureInput scale="c" />
            <TemperatureInput scale="f" />
          </div>
        );
      }
    }

  ```

### 5. global한 변환 함수 작성하기

```js
function toCelsius(fahrenheit) { ... };
function toFahrenheit(celsius) { ... };

// temp: string
// convert: function toCelsius or toFahrenheit
function tryConvert(temp, convert) {
  const input = parseFloat(temp); 
  if (Number.isNaN(input)) { return ''; }
  const output = convert(input);
  const rounded = Math.round(output * 1000) / 1000; 
  // 소수점 세번째 자리 반올림 
  return rounded.toString();
};
```

### 6. State 끌어올리기

- TemperatureInput 컴포넌트가 각각 state를 가지지 않고, 부모인 Calculator 로 state 를 옮기기
- Calculator 가 공유될 state를 소유하게 한다.

- TemperatureInput 컴포넌트의 render()에 있던 temperature state 를 props로 바꾼다: `const temp = this.props.temp` 
  - props 는 읽기 전용인 값이다.
  - 더 이상 TemperatureInput 클래스 컴포넌트가 직접 setState를 하지 않는다. 

- Calculator 컴포넌트
  - state: { temp, scale } 저장
  - TemperatureInput 에 temp, onTempChange props를 전달해준다.
    - input onChange ~ handleChange (TempInput) 에서 onTempChange (Cal) 를 호출한다
    - onTempChange (Cal) 이 hanldeCelsiusChange, handleFahrenheitChange (Cal) 를 호출해서, setState 한다.
    - setState 후, UI를 업데이트 하기 위해 Cal의 render 메서드를 리액트가 호출한다.
    - setState 해서 업데이트된 this.state.temp 값을 단위에 맞게 변환한 후, TemperatureInput 의 temp props 에 전달한다.