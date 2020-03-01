---
layout: post
categories: dev
title: "Golang 기초 개념: Function"
date: 2018-02-05T13:01:27-05:00
share: true
---

## Go Function

### Pass by Value

```Go
package main

func main() {
	msg := "Hello"
	println("original: ", msg)
	say(&msg)
	println("after say(&msg): ", msg)
}

func say(msg *string) {
	println("say function received: ", *msg)
	*msg = "Changed"
	println("star msg is: ", *msg)
}
```

### Pass by Reference
- &msg : **Reference**
  - msg가 저장된 메모리 영역의 주소를 접근한다
  - msg 변수 값을 변화시키면 &msg도 변한 값을 출력해준다.
- *msg : **Dereferencing**
  - msg 저장된 메모리 주소에 데이터를 쓰기 위해서 사용
  - 함수의 input으로 &msg 가 들어올 때, 함수의 인자를 *msg로 해줘야함

### Variadic Function 가변인자함수

- 다양한 숫자의 파라미터 전달
- 3개의 마침표 ...
  - ...string
  - 파이썬, 자바스크립트 ES6에서 볼 수 있는 애
  - n개의 동일타입 파라미터 전달 가능
- 이런 파라미터들을 받아들이는 함수가 가변인자함수

```Go
package main

func main() {
    say("This", "is", "a", "book")
    say("Hi")
}

// func say(msg ...string) {
//     for ind, s := range msg {
//         println(ind, ": ", s)
//     }
// }

func say(msg ...string) {
    for _, s := range msg {
        println(_, s)
    }
}

```
## 함수 리턴값
- 리턴 값: 0개, 1개, 다수 개 가능
- **Named Return Parameter**
- func 문: return s

```Go
package main
 
func main() {
    count, total := sum(1, 7, 3, 5, 9)
    println(count, ",", total)
}
 
func sum(nums ...int) (count int, total int) {
    for _, n := range nums {
        total += n
    }
    count = len(nums)
    return count, total
}
```

## Go 익명함수
### 익명함수
- JS ES6에서 본 듯함
- func main() 안에 또다른 func 함수를 변수 정의하듯이 정의하고 걔의 리턴 값을 main() 안에서 활용할 수 있지롱

### 일급함수
- 함수 자체가 다른 함수의 입력/리턴 파라미터가 될 수 있다

```Go
package main
 
func main() {
    //변수 add 에 익명함수 할당
    add := func(i int, j int) int {
        return i + j
    }
 
    // add 함수 전달
    r1 := calc(add, 10, 20) // add 함수의 리턴값이 r1에 저장되어 있음
    println(r1) // 30
 
    // 직접 첫번째 파라미터에 익명함수를 정의함
    r2 := calc(func(x int, y int) int { return x - y }, 10, 20) // a int, b int = 10, 20
	  // 새로운 함수 func - x, y를 인자로 받고, 리턴값 타입이 int, 리턴값은 x-y 
    println(r2) // -10
 
}
 
func calc(f func(int, int) int, a int, b int) int {
    result := f(a, b)
    return result
}
```

### type 문 사용한 함수 원형 정의

- struct 구조체, 인터페이스 등 custom type을 정의하기 위해 type을 사용한다.
- 함수 원형을 정의하는데 사용
  - 예를 들어, 위 예시에서 func(x int, y int) int 이렇게 줄줄이 인풋 파라미터에 쓴 것도 미리 '원형 정의' 하고 사용 가능
- 타 언어에서는 이렇게 함수의 원형을 정의하고, 이 함수를 타 메서드에 전달하고 리턴받는 기능을 'Delegate' 라고 부른다.

```Go
// 원형 정의
type calculator func(int, int) int
 
// calculator 원형 사용
func calc(f calculator, a int, b int) int {
    result := f(a, b)
    return result
}
```

## Closure
- 함수 바깥에 있는 변수를 참조하는 함수값 = function value
- 바깥의 변수를 마치 함수 안으로 끌어들인듯이 그 변수를 읽거나 쓸수 있다.

```Go
package main
 
func nextValue() func() int {   // int 리턴합니다.
    i := 0                // i를 아래에서 사용합니다.
    return func() int {   // 익명함수
        i++              // i가 계속 초기화되는 게 아니라 값++ 하나씩 증가.
        return i
    }
}
 
func main() {
    next := nextValue()
 
    println(next())  // 1
    println(next())  // 2
    println(next())  // 3
 
    anotherNext := nextValue()
    println(anotherNext()) // 1 다시 시작
    println(anotherNext()) // 2
}
```
