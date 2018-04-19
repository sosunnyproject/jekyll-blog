---
layout: default
---

# Windows machines (7 32bit, 10 64bit)

- unreal - win 32 bit not working & download website is blocked


## React (web) - listening port 

Need to kill 3000 port everytime i run 'npm start'....
https://stackoverflow.com/questions/39632667/how-to-kill-a-currently-using-port-on-localhost-in-windows
```s
$ netstat -ano | findstr :yourPortNumber
$ taskkill /PID typeyourPIDhere /F
```

## windows git bash

Windows - git bash 이용
**git bash problem with korean name user**
Make sure you're at MINGW32:/ or 64:/ the very first node
```s
$ cd /c/Users
$ cd 박\ 소선/   #성 입력 후 tab 하면 자동으로 \ 붙여줌
$ cd Desktop
```
DONE!

## yarn add firebase 에러

firebase를 추가한 후 에러가 자꾸 나서 yarn으로 했더니 더 이상한 에러..
package.json에서 뺴고, ./app/package.json에다가 설치하는게 가장 좋은 방법 인듯.

아래 터미널에서는 python어쩌고 에러..(윈도우여서 생기는 에러가 아닐까 싶음...)

```s
$ yarn add firebase@4.2.0
yarn add v1.3.2
[1/4] Resolving packages...
[2/4] Fetching packages...
info 7zip-bin-linux@1.1.0: The platform "win32" is incompatible with this module
.
info "7zip-bin-linux@1.1.0" is an optional dependency and failed compatibility c
heck. Excluding it from installation.
info 7zip-bin-mac@1.0.1: The platform "win32" is incompatible with this module.
info "7zip-bin-mac@1.0.1" is an optional dependency and failed compatibility che
ck. Excluding it from installation.
info fsevents@1.1.1: The platform "win32" is incompatible with this module.
info "fsevents@1.1.1" is an optional dependency and failed compatibility check.
Excluding it from installation.
[3/4] Linking dependencies...
warning " > react-desktop@0.3.3" has unmet peer dependency "prop-types@^15.0 ||
^16.0".
warning " > extract-text-webpack-plugin@2.1.2" has incorrect peer dependency "we
bpack@^2.2.0".
warning "jsdom > request-promise-native@1.0.4" has unmet peer dependency "reques
t@^2.34".
warning "jsdom > request-promise-native > request-promise-core@1.1.1" has unmet
peer dependency "request@^2.34".
[4/4] Building fresh packages...
[-/5] ⢀ waiting...
[-/5] ⢀ waiting...
[-/5] ⢀ waiting...
[4/5] ⢀ node-sass: Build failed with error code: 1
error C:\Users\박 소선\Desktop\demo\elect-react-bp-test\node_modules\node-sass:
Command failed.
Exit code: 1
Command: node scripts/build.js
Arguments:
Directory: C:\Users\박 소선\Desktop\demo\elect-react-bp-test\node_modules\node-s
ass
Output:
Building: C:\Program Files\nodejs\node.exe C:\Users\박 소선\Desktop\demo\elect-r
eact-bp-test\node_modules\node-gyp\bin\node-gyp.js rebuild --verbose --libsass_e
xt= --libsass_cflags= --libsass_ldflags= --libsass_library=
gyp info it worked if it ends with ok
gyp verb cli [ 'C:\\Program Files\\nodejs\\node.exe',
gyp verb cli   'C:\\Users\\박 소선\\Desktop\\demo\\elect-react-bp-test\\node_mod
ules\\node-gyp\\bin\\node-gyp.js',
gyp verb cli   'rebuild',
gyp verb cli   '--verbose',
gyp verb cli   '--libsass_ext=',
gyp verb cli   '--libsass_cflags=',
gyp verb cli   '--libsass_ldflags=',
gyp verb cli   '--libsass_library=' ]
gyp info using node-gyp@3.6.2
gyp info using node@9.3.0 | win32 | ia32
gyp verb command rebuild []
gyp verb command clean []
gyp verb clean removing "build" directory
gyp verb command configure []
gyp verb check python checking for Python executable "python2" in the PATH
gyp verb `which` failed Error: not found: python2
gyp verb `which` failed     at getNotFoundError (C:\Users\박 소선\Desktop\demo\e
lect-react-bp-test\node_modules\which\which.js:13:12)
gyp verb `which` failed     at F (C:\Users\박 소선\Desktop\demo\elect-react-bp-t
est\node_modules\which\which.js:68:19)
gyp verb `which` failed     at E (C:\Users\박 소선\Desktop\demo\elect-react-bp-t
est\node_modules\which\which.js:80:29)
gyp verb `which` failed     at C:\Users\박 소선\Desktop\demo\elect-react-bp-test
\node_modules\which\which.js:89:16
gyp verb `which` failed     at C:\Users\박 소선\Desktop\demo\elect-react-bp-test
\node_modules\isexe\index.js:42:5
gyp verb `which` failed     at C:\Users\박 소선\Desktop\demo\elect-react-bp-test
\node_modules\isexe\windows.js:36:5
gyp verb `which` failed     at FSReqWrap.oncomplete (fs.js:166:21)
gyp verb `which` failed  python2 { Error: not found: python2
gyp verb `which` failed     at getNotFoundError (C:\Users\박 소선\Desktop\demo\e
lect-react-bp-test\node_modules\which\which.js:13:12)
gyp verb `which` failed     at F (C:\Users\박 소선\Desktop\demo\elect-react-bp-t
est\node_modules\which\which.js:68:19)
gyp verb `which` failed     at E (C:\Users\박 소선\Desktop\demo\elect-react-bp-t
est\node_modules\which\which.js:80:29)
gyp verb `which` failed     at C:\Users\박 소선\Desktop\demo\elect-react-bp-test
\node_modules\which\which.js:89:16
gyp verb `which` failed     at C:\Users\박 소선\Desktop\demo\elect-react-bp-test
\node_modules\isexe\index.js:42:5
gyp verb `which` failed     at C:\Users\박 소선\Desktop\demo\elect-react-bp-test
\node_modules\isexe\windows.js:36:5
gyp verb `which` failed     at FSReqWrap.oncomplete (fs.js:166:21) code: 'ENOENT
' }
gyp verb check python checking for Python executable "python" in the PATH
gyp verb `which` failed Error: not found: python
gyp verb `which` failed     at getNotFoundError (C:\Users\박 소선\Desktop\demo\e
lect-react-bp-test\node_modules\which\which.js:13:12)
gyp verb `which` failed     at F (C:\Users\박 소선\Desktop\demo\elect-react-bp-t
est\node_modules\which\which.js:68:19)
gyp verb `which` failed     at E (C:\Users\박 소선\Desktop\demo\elect-react-bp-t
est\node_modules\which\which.js:80:29)
gyp verb `which` failed     at C:\Users\박 소선\Desktop\demo\elect-react-bp-test
\node_modules\which\which.js:89:16
gyp verb `which` failed     at C:\Users\박 소선\Desktop\demo\elect-react-bp-test
\node_modules\isexe\index.js:42:5
gyp verb `which` failed     at C:\Users\박 소선\Desktop\demo\elect-react-bp-test
\node_modules\isexe\windows.js:36:5
gyp verb `which` failed     at FSReqWrap.oncomplete (fs.js:166:21)
gyp verb `which` failed  python { Error: not found: python
gyp verb `which` failed     at getNotFoundError (C:\Users\박 소선\Desktop\demo\e
lect-react-bp-test\node_modules\which\which.js:13:12)
gyp verb `which` failed     at F (C:\Users\박 소선\Desktop\demo\elect-react-bp-t
est\node_modules\which\which.js:68:19)
gyp verb `which` failed     at E (C:\Users\박 소선\Desktop\demo\elect-react-bp-t
est\node_modules\which\which.js:80:29)
gyp verb `which` failed     at C:\Users\박 소선\Desktop\demo\elect-react-bp-test
\node_modules\which\which.js:89:16
gyp verb `which` failed     at C:\Users\박 소선\Desktop\demo\elect-react-bp-test
\node_modules\isexe\index.js:42:5
gyp verb `which` failed     at C:\Users\박 소선\Desktop\demo\elect-react-bp-test
\node_modules\isexe\windows.js:36:5
gyp verb `which` failed     at FSReqWrap.oncomplete (fs.js:166:21) code: 'ENOENT
' }
gyp verb could not find "python". checking python launcher
gyp verb could not find "python". guessing location
gyp verb ensuring that file exists: C:\Python27\python.exe
gyp ERR! configure error
gyp ERR! stack Error: Can't find Python executable "python", you can set the PYT
HON env variable.
gyp ERR! stack     at PythonFinder.failNoPython (C:\Users\박 소선\Desktop\demo\e
lect-react-bp-test\node_modules\node-gyp\lib\configure.js:483:19)
gyp ERR! stack     at PythonFinder.<anonymous> (C:\Users\박 소선\Desktop\demo\el
ect-react-bp-test\node_modules\node-gyp\lib\configure.js:508:16)
gyp ERR! stack     at C:\Users\박 소선\Desktop\demo\elect-react-bp-test\node_mod
ules\graceful-fs\polyfills.js:284:29
gyp ERR! stack     at FSReqWrap.oncomplete (fs.js:166:21)
gyp ERR! System Windows_NT 6.1.7601
gyp ERR! command "C:\\Program Files\\nodejs\\node.exe" "C:\\Users\\박 소선\\Desk
top\\demo\\elect-react-bp-test\\node_modules\\node-gyp\\bin\\node-gyp.js" "rebui
ld" "--verbose" "--libsass_ext=" "--libsass_cflags=" "--libsass_ldflags=" "--lib
sass_library="
gyp ERR! cwd C:\Users\박 소선\Desktop\demo\elect-react-bp-test\node_modules\node
#NAME?
gyp ERR! node -v v9.3.0
gyp ERR! node-gyp -v v3.6.2
```

## electron-react-boilerplate 사용 (윈도우)
```s
$ git clone --depth=1 https://github.com/chentsulin/electron-react-boilerplate bp-test
$ cd bp-test
$ npm run build
#왜인지 모르겠지만 win32 7 에서는 바로 npm run dev 하면 안되고 매번 실행할때마다 npm run build 를 해줘야지 npm run dev해서 창이 뜨더랏..
$ npm run dev
```

## facebook이 만든 리액트 앱의 뼈대 repo. 
https://github.com/facebookincubator/create-react-app
가장 기본적인 것들 자질구레잡다한거 다 빌드해놨으니 이 위에다가 얹어서 빌드하셈.

#### 교훈: 윈도우 7 절레절레

```s
$ cd Desktop 
$ cd demo
#demo is the name of my folder
$ npm install -g create-react-app
#create-react-app은 리액트 앱의 기초 뼈대를 이미 만들어놓은 패키지. https://github.com/facebookincubator/create-react-app 참조
$ yarn global add create-react-app
$ create-react-app #name#
$ cd #name#
$ yarn start
$ create-react-app vel-tut

Creating a new React app in C:\Users\박 소선\Desktop\demo\vel-tut.

Installing packages. This might take a couple of minutes.
Installing react, react-dom, and react-scripts...

yarn add v1.3.2
info No lockfile found.
[1/4] Resolving packages...
[2/4] Fetching packages...
info fsevents@1.1.2: The platform "win32" is incompatible with this module.
info "fsevents@1.1.2" is an optional dependency and failed compatibility check. Excluding it from installation.
info fsevents@1.1.3: The platform "win32" is incompatible with this module.
info "fsevents@1.1.3" is an optional dependency and failed compatibility check. Excluding it from installation.
[3/4] Linking dependencies...
error An unexpected error occurred: "EPERM: operation not permitted, lstat 'C:\\Users\\박 소선\\Desktop\\demo\\vel-tut\\node_modules\\recursive-readdir\\test\\testsymlinks\\linkeddir\\hi.docx'".
info If you think this is a bug, please open a bug report with the information provided in "C:\\Users\\박 소선\\Desktop\\demo\\vel-tut\\yarn-error.log".
info Visit https://yarnpkg.com/en/docs/cli/add for documentation about this command.

Aborting installation.
  yarnpkg add --exact react react-dom react-scripts --cwd C:\Users\박 소선\Desktop\demo\vel-tut has failed.

Deleting generated file... node_modules
Deleting generated file... package.json
Deleting generated file... yarn-error.log
Deleting vel-tut / from C:\Users\박 소선\Desktop\demo
Done.
```

