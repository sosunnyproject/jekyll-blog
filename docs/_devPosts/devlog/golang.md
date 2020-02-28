---
title: "GoLang Study"
categories:
  - dev
tags:
  - dev
  - golang
last_modified_at: 2017-03-09T13:01:27-05:00
---

C:\Go\bin에서 test.go 메모장으로 만들어서 돌리는 데 계속 에러낭
- `can't load package: package main: read C:\Go\bin\test.go: unexpected NUL in input`
- test.go 메모장으로 만든걸 vscode로 열려했더니 이진수 어쩌고 하면서 안열림
- 메모장 코드 파일 지우고, vscode로 아예 test.go 생성해서 만듬
- go run test.go 했더니 성공 (UTF-8 의 문제라는 얘기들이 있어서 메모장 버렸더니, 잘됨)

GOPATH, GOROOT
- gopath: workspace 폴더 여러개 지정 가능
- goroot: go 가 설치된 디렉토리

Eclipse, VS code 에서 GO 패키지 환경 설정
- Go and Eclipse
    - https://github.com/GoClipse/goclipse/blob/latest/documentation/Installation.md#installation
    - http://golang.site/go/article/204-Eclipse%EC%97%90%EC%84%9C-Go-%EC%82%AC%EC%9A%A9
- Go and VSCode: http://golang.site/go/article/203-VS-Code%EC%97%90%EC%84%9C-Go-%EC%82%AC%EC%9A%A9

Go 언어
- package main func main()
    - 설명: 첫라인은 함수들(여기서는 main 하나)이 소속된 패키지명(main)을 지정하는 것이고, 다음 라인의 func main() 은 메인함수를 정의한 것이다. Go는 main 패키지 내의 Entry Point인 main() 함수를 찾아 프로그램을 실행한다. 
    - from: http://golang.site/go/article/3-Go-%EA%B0%84%EB%8B%A8%ED%95%9C-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8-%EC%9E%91%EC%84%B1
    - 

guru.exe가 안깔려서 겁나 헤맨 에러..
- GOPATH 에 src, bin, pkg 폴더를 억지로 만들지 말것.
    - 아마 bin은 자동 생성 되긴 할텐데, src, pkg는 아닐것임
    - 나의 경우 src, pkg 까지 수동으로 생성해줫더니, 잘못나온듯.
- 수동으로 한게 없는데도 이런 에러가 난다면: 
 ```bash
C:\Go $ go get -v golang.org/x/tools/cmd/guru

Fetching https://golang.org/x/tools/cmd/guru?go-get=1
Parsing meta tags from https://golang.org/x/tools/cmd/guru?go-get=1 (status code 200)
get "golang.org/x/tools/cmd/guru": found meta tag get.metaImport{Prefix:"golang.org/x/tools", VCS:"git", RepoRoot:"https://go.googlesource.com/tools"} at https://golang.org/x/tools/cmd/guru?go-get=1
get "golang.org/x/tools/cmd/guru": verifying non-authoritative meta tag
Fetching https://golang.org/x/tools?go-get=1
Parsing meta tags from https://golang.org/x/tools?go-get=1 (status code 200)
golang.org/x/tools (download)
# cd D:\eclipse\eclipse-oxygen-workspace\go\src\golang.org\x\tools; git pull --ff-only
fatal: No remote repository specified.  Please, specify either a URL or a
remote name from which new revisions should be fetched.
package golang.org/x/tools/cmd/guru: exit status 1`
```
- 나는 환경변수에서 GOPATH 가 D:\eclipse\....\go 되어 있던 것에다가 \bin 더해줌.
    - 그리고 위 커맨드 다시 돌렸더니, bin 폴더 아래에 bin, src 만들어서 tools 다 다운받음
    - 새로 생긴 go\bin\src 파일을 내가 수동으로 만든 go\src 파일 위에 엎어버림
    - go\bin\bin 에는 guru.exe만 깔렸을 거임. 이 guru.exe를 ctrl+x 해서 상위 go\bin 폴더로 옮겨버리고, 하위에 새로 생긴 go\bin\bin은 지워버리셈.


- 그리고 VScode 에서 Analysis Tool Missing 떠서 install 눌렀는데 자꾸 failed 뜨면
  - 우선 위처럼 내가 매뉴얼로 만든 건 아닌지 확인해보고
  - 환경변수에서 GOPATH 에다가 your-directory-path\go 워크스페이스 원래 주소 냅두고 그 뒤에 ;your-directory-path\go\bin 도 추가해주기.
    - 나의 경우 이렇게 해줬더니 install 할때 잘됐음: 이런 메시지 뜨면서
      - `Installing 5 tools at D:\eclipse\eclipse-oxygen-workspace\go;\bin`
      