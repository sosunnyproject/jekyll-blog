## Go Struct

- custom data type을 표현: 필드들의 집합체, 필드들의 컨테이너
- Go에서 Struct는 필드 데이타만을 가진자
- 행위를 표현하는 메서드를 갖지 않는다.
- Go만의 방식을 가진 OOP 이다
    - 클래스, 객체, 상속 개념이 없다
    - 메소드는 struct와 별개로 분리하여 정의

### Struct 선언
- type 문 사용해서 Custom Type 정의
- struct 명 쓰기
    - 대문자: public, 소문자: private
- struct 타입으로 객체 생성하기
    - struct 필드를 액세스하기 위해 .(dot)을 사용한다.
    - person 객체를 먼저 할당
- new() 내장함수 사용해서 
    - 모든 필드를 zero value로 초기화
    - 객체의 포인터(*person)을 리턴한다.
    - 포인터라도, 필드 액세스는 .(dot)사용
        - 이 때, 포인터는 자동 dereference 된다
- struct는 mutable한 개체
    - 필드값이 변화하면, 해당 개체 메모리에서 직접 변경
    - struct 개체를 다른 함수의 parameter로 넘기면: Pass by Value로 객체 복사 및 전달
    - struct의 포인터를 전달하면: Pass by Reference

```Go
package main 
import "fmt"

// struct 정의
type person struct {
    name string
    age  int
}
 
func main() {
    // person 객체 생성
    p := person{}
     
    // 필드값 설정
    p.name = "Lee"
    p.age = 10
     
    fmt.Println(p)

    // struct 객체 생성하면서 초기값 함께 할당
    p1 := person{}
    p1 = person{"Bob", 20}
    fmt.Println(p1)

    // 필드명(named field) 지정하고 값 넣기 
    p2 := person{name: "Sean", age: 17}
    fmt.Println(p2)

    // new() 사용하면 모든 필드는 zero value 초기화
    // person 객체의 포인터 (*person) 리턴한다.
    // 위에서 이미 지정했던 p, p1, p2 이런애들을 초기화하려고 하면 에러난다.
    p3 := new(person)
    p3.name ="Park"
    fmt.Println(*p3)
}
```
### 생성자 함수 constructor
- struct 의 필드가 사용 전에 초기화되어야하는 경우
- 생성자 함수는 struct를 리턴한다.
    - 본문에서 필요한 필드를 초기화한다.

- newDict() dict라는 struct의 map필드를 초기화한다. 
- struct 포인터를 리턴한다.
    - 내용물 println 하고 싶다면 `fmt.Println(*dic)`

## Go 메서드
- 특별한 형태의 func 함수이다
- receiver 부분: 이 메서드가 속한 struct 타입과 struct 변수명 지정
  - struct 변수명은 그 메서드 내에서 마치 입력 parameter 처럼 사용된다.
  - Rect라는 struct를 정의하고 area() 메서드를 정의하고 있다.
  - Rect 구조체(struct)의 객체(rect in func main())는 .area() 메소드 직접 호출 가능.

```Go
package main 

type Rect struct {
    width, height int
}

func (r Rect) area() int {
    return r.width * r.height
}

func main() {
    rect := Rect{10, 20}
    area := rect.area()  // 객체가 직접 메소드 소환 가능
    println(area)
}
```
### value VS. pointer receiver
- struct의 데이터를 복사하여 전달하며 포인터 receiver 는 struct의 포인터만을 전달한다.
- value receiver: 메서드 내에서 그 struct의 필드값이 변경되더라도 호출자의 데이타는 변경 안됨.
- pointer receiver: 메서드 내의 필드값 변경이 그대로 호출자에서 반영

```Go
package main
 
//Rect - struct 정의
type Rect struct {
    width, height int
}

//Pointer Receiver
func (r *Rect) area2() int {
    r.width++
    return r.width * r.height
}

func main() {
    rect := Rect{10, 20}
    area := rect.area2() //메서드 호출
    println(rect.width, area) // 11 220 출력
}
```

## Go 인터페이스
- struct가 필드들의 집합체
- interface는 메서드들의 집합체
  - type이 구현해야 하는 **method prototype** 정의

```Go
type Shape interface {
    area() float64  
    perimeter() float64 
}

// interface의 struct, method 정의
type Rect struct {
    width, height float64
}
 
//Circle 정의
type Circle struct {
    radius float64
}
 
//Rect 타입에 대한 Shape 인터페이스 구현 
func (r Rect) area() float64 { return r.width * r.height }
func (r Rect) perimeter() float64 {
     return 2 * (r.width + r.height)
}
 
//Circle 타입에 대한 Shape 인터페이스 구현 
func (c Circle) area() float64 { 
    return math.Pi * c.radius * c.radius
}
func (c Circle) perimeter() float64 { 
    return 2 * math.Pi * c.radius
}

// 인터페이스 사용
func main() {
    r := Rect{10., 20.}
    c := Circle{10}
    showArea(r, c)
}

func showArea(shapes ...Shape) {  // input param # can be any
    for _, s := range shapes {b  // _ is index 0,1,2...
        a := s.area() //인터페이스 메서드 호출
        println(a)
    }
}
```

### 인터페이스 타입
- Empty interface: interface{}
  - 함수 prototype 보면 empty interface 자주 등장
  - 메서드를 전혀 갖지 않음
  - Go 의 모든 Type은 적어도 0개의 메서드 구현. Go 에서 모든 type 나타내기 위해 빈 인터페이스 사용
  - Dynamic Type
    - 어떠한 타입도 담을 수 있다.
    - c#, java: object / c, c++: void*

### Type Assertion
- interface type: x, T에 대해서 x.(T)
- x가 nil이 아니며, x는 T 타입에 속한다 는 것을 assert하는 것.
  - x가 T타입이 아닐 경우: runtime error
  - x가 T타입이 맞을 경우: T타입의 x를 리턴
```Go
package main


func main() {
    var a interface{} = 3
    // ~~~ 3 대신 "hello"라고 썼으면 ~~~

    i := a       // a와 i 는 dynamic type, 값은 1
    j := a.(int) // j는 int 타입, 값은 1
    // ~~~ 여기서 에러 났을 것 ~~~

    println(i)  // 포인터주소 출력
    println(j)  // 1 출력
}
```

## Go 에러
- error 라는 interface 타입
- error 인터페이스를 주고 받게 되는데, 이 interface 다음과 같은 하나의 메서드를 갖는다. 
  - `type error interface { Error() string }`

## Go defer
- defer 함수: 마지막에 clean-up 작업을 위해 사용된다
- panic 함수: 현재 함수 멈추고, 현재 함수의 defer 함수들 모두 실행 후 즉시 리턴, 에러 내고 종료
- recover 함수: 패닉 상태를 정상 상태로 되돌림. 패닉 상태 제거, 다음 문장 실행

## Go 루틴, Go 채널, 등
- Go 런타임이 관리하는 Lightweight 논리적(가상) 쓰레드
- 비동기 통신 등 사용시에 더 찾아볼 것.