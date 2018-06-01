## Go 컬렉션 - 배열

- 고정된 배열크기 안에 동일한 타입읟 데이터 연속 저장
- 배열의 크기를 다이나믹하게 증가하거나 부분 배열 발췌 같은 기능을 불가

```Go
package main
 
func main() {
    var a [3]int  //정수형 3개 요소를 갖는 배열 a 선언
    a[0] = 1
    a[1] = 2
    a[2] = 3
    println(a[1]) // 2 출력

    var a1 = [3]int{1, 2, 3}
    var a3 = [...]int{1, 2, 3} //배열크기 자동으로
    println(a1[0], a1[1], a1[2])
    println(len(a3))

    var b = [2][3]int{
        {1, 2, 3},
        {4, 5, 6},  //끝에 콤마 추가
    }
    println(b[1][2])
}
```

## Go 컬렉션 - Slice

- 배열의 한계점 극복
- 크기 지정 안함
- 크기 변경 가능
- 부분 배열 발췌 가능
- 정수형 Slice 변수 a를 선언: `var a []int`

```Go
package main
import "fmt"
 
func main() {
    var a []int        //슬라이스 변수 선언
    a = []int{1, 2, 3} //슬라이스에 리터럴값 지정
    a[1] = 10
    fmt.Println(a)     // [1, 10, 3]출력
}
```

- **Package fmt implements formatted I/O with functions analogous to C's printf and scanf.**

### slice : make()

- Slice 생성할 때: 내장함수 make() 함수 사용 가능
  - make() 쓰면 Slice의 length, capacity 임의로 지정 가능
  - len() : length: Slice의 길이, cap(): Capacity: 내부 배열의 최대 길이
  - 모든 요소는 디폴트로 Zero value
  - Capacity 생략하면 Length와 같은 값
- make()의 첫번째 인자는 type을 넣어야함

```Go
package main
import "fmt"

func main() {
	s := make([]int, 5)
	println(len(s), cap(s)) // len 5, cap 10
	s[0], s[1], s[2], s[3], s[4] = 0, 1, 2, 3, 4
    fmt.Println(s)
    // 5 5
    // [0 1 2 3 4]
}
```

### slice : sub-slice
- python과 비슷
- 처음인덱스:마지막인덱스 like [a:b]
- 처음인덱스(a)는 포함, 마지막인덱스(b)는 제외

```Go
package main
import "fmt"

func main() {
  s:= []int{0,1,2,3,4}
  s = s[1:4]
  fmt.Println(s)
  // [1 2 3]
  a := s[1:]
  fmt.Println(a)
  // [2 3]
}
```

### slice: 추가, append(병합), copy(복사)

- append()할 때, capacity 를 초과하는 경우
  - cap()이 남아 있다면 len()을 변경해서 데이터 추가
  - cap()이 남아있지 않다면
    - 초기 cap()값이 아닌, 현재 len() 값의 두배 만큼 cap()이 늘어난다.
    - 예를 들어, len=3 cap=3 인 상황에서 1개를 append하면 len=4 가 되고 싶어할 것
      - cap()은 이 len의 2배만큼 늘어난다.
      - 즉 (len 3, cap 3)에 append 하나를 더 하면 (len 4, cap 8)이 된다.
      
```Go
package main
import "fmt"

func main() {
    // len=0, cap=3 인 슬라이스
    sliceA := make([]int, 0, 3)
 
    // 계속 한 요소씩 추가
    for i := 1; i <= 15; i++ {
        fmt.Println(len(sliceA), cap(sliceA))
        sliceA = append(sliceA, i)
        // 슬라이스 길이와 용량 확인
        fmt.Println(len(sliceA), cap(sliceA))
        fmt.Println(sliceA)
    }
 
    fmt.Println(sliceA) // 1 부터 15 까지 숫자 출력 
}
```

- 두개의 슬라이스를 합칠 때
  - `sliceB...` syntax에 유념할 것

```Go
package main
 
import "fmt"
 
func main() {
    sliceA := []int{1, 2, 3}
    sliceB := []int{4, 5, 6}
 
    sliceA = append(sliceA, sliceB...)
    //sliceA = append(sliceA, 4, 5, 6)
 
    fmt.Println(sliceA) // [1 2 3 4 5 6] 출력
}
```

- copy() 사용해서 한 슬라이스를 다른 슬라이스로 복사
- _슬라이스는 실제 배열을 가리키는 포인터 정보만을 가진다._ 
- **즉, 소스 슬라이스가 갖는 배열의 데이타를 타겟 슬라이스가 갖는 배열로 복제하는 것임)**

### slice: 내부구조
- **슬라이스는 내부적으로 사용하는 배열의 부분 영역인 세그먼트에 대한 메타 정보를 가지고 있다.**

슬라이스를 구성하는 3개의 필드
1. 내부적으로 사용하는 배열에 대한 포인터 (--> 내부 배열)
2. 세그먼트 길이 (length)
3. 세그먼트의 최대 용량(capacity)
  - 처음에 슬라이스 만들 때, 용량 만큼 배열을 생성함.


## Go 콜렉션 - Map

1. Map 개요
- Map: Key, Value 를 신속히 찾는 해시테이블을 구현한 자료구조
- Go 언어: Map 내장

```Go
var idMap map[int]string
idMap = make(map[int]string)
```

## Go 패키지

- 코드의 모듈화, 코드의 재사용 기능 제공
- 작은 단위의 컴포넌트 작성, 작은 패키지 활용해서 프로그램 작성

## Main 패키지
- "main"이라고 망명된 패키지는 Go Compiler 특별하게 인식됨.
- 컴파일러가 main 패키지를 executable 프로그램으로 만든다.
- main() 함수가 main 패키지의 entry point, 프로그래밍 시작점
- 공유 라이브러리로 만들꺼면 main 패키지/main() 함수 쓰면 안됨.

### 패키지 import
- 패키지 임포트 할 때: GOROOT, GOPATH 환경변수를 검색.
- 표준 패키지는 GOROOT/pkg
- 사용자/제3자 패키지는 GOPATH/pkg

### 패키지 scope
- 함수, 구조체, 인터페이스, 메서드
- identifier 첫문자를 
    - 대문자로 시작: public으로 사용 가능
    - 소문자: non-public, 패키지 내부

### 패키지 init 함수, alias
- 패키지 작성
- import _ "package-name" : init()만 import
- import ( mongo "/../../")

### 사용자 정의 패키지 생성
- 폴더하나에 .go 파일들 묶기
- 패키지명 = 폴더명
