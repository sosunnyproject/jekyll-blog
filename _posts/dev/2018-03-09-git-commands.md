---
title: "Git Commands"
layout: post
categories:
  - dev
tags:
  - dev
  - firebase
last_modified_at: 2018-03-09T13:01:27-05:00
---

## github README.md markdown
https://stackoverflow.com/questions/19699059/representing-directory-file-structure-in-markdown-syntax

## git branch

1. git checkout diff local branch without saving the change in current local branch		
https://stackoverflow.com/questions/1304626/git-switch-branch-and-ignore-any-changes-without-committing			

```s	
$ git checkout -f				
$ git checkout branch-name				
```

2. When i dont have a remote branch (not master) in my local repo. (BUT this auto-saves THE remote branch into your local repo)

```s
$ git checkout -b firebase-test origin/firebase-test				
```

## git remote repo's non-master branches 

**방법 1**
git >= 1.6.6 부터는 그냥 같은 이름의 브랜치를 local 에다가 만들면
그 안에 같은 이름의 remote branch 가 다 뜬다.
```s
$ git checkout uitest 
#했더니 Branch uitest set up to track remote branch uitest from origin. Switched to a new branch 'uitest' 배출

#아니면…
#(master)
$ git fetch origin
$ git branch -v -a
$ git checkout -b uitest origin/uitest
```

**방법 2**
```s
$ git clone your-git-remote-repo-address.git --depth=1
이때 모든 브랜치도 다 다운받음 (최신 git 버젼에서는.)
$ git fetch origin 
(혹시나 원하면..)
$ git branch
master 만 나올것임.
$ git checkout uitest 
```
참고로 uitest는 remote repo의 non-master branch의 이름. checkout 하면 자동으로 생기면서 그 안에다가 해당 uitest branch 정보 다 저장함. 단, remote repo의 branch 와 반드시 이름이 같도록 설정하긔.


#### 멍청한 노가다 구글링...
git clone specific branch?
https://stackoverflow.com/questions/1778088/how-to-clone-a-single-branch-in-git/4146786#4146786
https://stackoverflow.com/questions/41233378/cloning-specific-branch/41234259

```s
$ git init
$ git remote add -t $BranchNameinYourGithubRepo -f origin $Remote-Repo-url
$ git pull origin $BranchName

#(하면 master branch에 remote-repo-branch 가 들어가있음)
$ git clone -b uitest --single-branch ~~~주소 ~~~  --depth 1
```
##### another 노가다 구글링 & 시행착오 (따라할 필요 없음)

1. 새로운 폴더를 만든다. 생성한 폴더의 master 브랜치에 remote repo의 uitest 브랜치가 복제된다.

```s
$ mkdir new
$ cd new
$ git init
$ git remote add -t uitest -f origin https://github.com/poscoict-arvrmr/second.git
$ git pull origin master
```

2. 기존 master가 있는 폴더에 uitest 브랜치를 추가한다.현재 브랜치는 master.

```s
$ git clone -b uitest --single-branch https://github.com/poscoict-arvrmr/second.git --depth 1
$ git checkout uitest
```

하면 uitest 라는 브랜치가 생겼고, 그 안에 remote branch 내용이 복제되어 있다. master 브랜치와 master의 본래 내용은 그대로 살아있다.


## merge the updated boilerplate repo while saving my edits on top of previous boilerplate version

처음에 clone한 boilerplate가 update되어서
내가 다운받은 boilerplate에 edit 한 버젼과 합치고 싶었음.
즉 두개의 다른 repositories 를 합치는 과정

A - 공식 boilerplate GIT (update 되었음)
B - 내가 edit한 boilerplate 버젼


@edit-bp2 :: master branch
```s
$ git remote rm origin
$ git remtoe add origin https://github.com/chentsulin/electron-react-boilerplate 원조 깃
$ git checkout master
$ git branch -m master-holder (이름 바꾸기)

$ git branch
# master-holder

$git fetch 
#하면 내가 remote 주소를 바꿨으니 , 그 주소에서 파일을 다 가져옴.
#git checkout master
$git pull origin master
$git merge master-holder
#하면 에러날거임. fatal: refusing to merge unrelated histories
#그래서..
$ git merge --allow-unrelated-histories master-holder
#automatic merge failed; fix conflicts and then commit the result.
#(자동 merge를 못했는데 npm install 을 돌리니 당연히 에러발생. 
#>>>>HEAD 이딴 코드 있어서 못읽고 토해버림.
 
#자동으로 merge를 못시켜주고 결국 충돌나는 코드들을 하나하나 내가 save해줌.  그 코드들에 들어가면 
#>>>>>HEAD
#>>>>>master-holder
#이렇게 뜨는데 한글로는 HEAD가 현재 변경 (원조 깃의 업뎃 버젼)
#master-holder (원래 기존의 edit-bp)가 수신 변경이다.
```
그래서 나는 내가 edit해서 살리고 싶은 코드들만 남기고 다 HEAD 현재변경을 택했음. 
그리고 다시 npm install..

https://gist.github.com/msrose/2feacb303035d11d2d05#combining-two-git-repositories
https://stackoverflow.com/questions/1425892/how-do-you-merge-two-git-repositories
extra: https://stackoverflow.com/questions/43205981/git-how-to-update-local-repository-and-keep-my-changes


## merge two different repos

merge two different repos
https://saintgimp.org/2013/01/22/merging-two-git-repositories-into-one-repository-without-losing-file-history/


change the git branch1 to master (hard overwrite)
https://stackoverflow.com/questions/2763006/make-the-current-git-branch-a-master-branch


master외의 브랜치를 merge하기 전에 따로 다운로드 받아 실행하고 싶은 경우에는 다음 중 하나를 선택해서 커맨드를 따라하세요.
