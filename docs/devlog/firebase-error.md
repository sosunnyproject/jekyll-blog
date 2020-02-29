---
layout: default
---

> also here: https://github.com/poscoict-arvrmr/docs/blob/master/note/second-manual20180124.md 

### 주의사항

firebase 는 ./package.json 에서 지우고, ./app/package.json 에서 install

```s
$ npm uninstall firebase
$ cd app
$ npm install firebase --save
```

### 지옥의 빌드 터미널

#### firebase 고치는 과정.

firebase는 ./app 에 넣으라고 친절하게 설명이 뜸.
$ npm uninstall firebase
$ cd app
$ npm install firebase --save

```s
firebase is a native dependency and should be installed inside of the "./app" folder.

First uninstall the packages from "./package.json":
npm uninstall your-package

Then, instead of installing the package to the root "./package.json":
npm install your-package --save

Install the package to "./app/package.json"
cd ./app && npm install your-package --save


Read more about native dependencies at:
https://github.com/chentsulin/electron-react-boilerplate/wiki/Module-Structure----Two-package.json-Structure



npm ERR! code ELIFECYCLE
npm ERR! errno 1
npm ERR! second@1.0.0 postinstall: `node -r babel-register internals/scripts/CheckNativeDep.js && npm run flow-typed && npm run build-dll && electron-builder install-app-deps && node node_modules/fbjs-scripts/node/check-dev-engines.js package.json`
npm ERR! Exit status 1
npm ERR!
npm ERR! Failed at the second@1.0.0 postinstall script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     /home/sosun/.npm/_logs/2018-01-25T08_35_45_955Z-debug.log
sosun@poscoict:~/Desktop/demo/second$ cd ./package.json
bash: cd: ./package.json: Not a directory
sosun@poscoict:~/Desktop/demo/second$ ls
app           flow-typed  node_modules       README.md  webpack.config.base.js       webpack.config.renderer.dev.dll.js  yarn.lock
appveyor.yml  internals   package.json       resources  webpack.config.eslint.js     webpack.config.renderer.dev.js
dll           LICENSE     package-lock.json  test       webpack.config.main.prod.js  webpack.config.renderer.prod.js
sosun@poscoict:~/Desktop/demo/second$ cd package.json
bash: cd: package.json: Not a directory
sosun@poscoict:~/Desktop/demo/second$ npm uninstall firebase
npm WARN deprecated gulp-util@3.0.8: gulp-util is deprecated - replace it, following the guidelines at https://medium.com/gulpjs/gulp-util-ca3b1f9f9ac5
npm WARN deprecated github@0.2.4: 'github' has been renamed to '@octokit/rest' (https://git.io/vNB11)
npm WARN deprecated graceful-fs@3.0.11: please upgrade to graceful-fs 4 for compatibility with current and future versions of Node.js
npm WARN postcss-html@0.12.0 requires a peer of postcss-less@>=1.1.0 but none is installed. You must install peer dependencies yourself.
npm WARN postcss-html@0.12.0 requires a peer of sugarss@>=1.0.0 but none is installed. You must install peer dependencies yourself.
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: 7zip-bin-win@2.1.1 (node_modules/7zip-bin-win):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for 7zip-bin-win@2.1.1: wanted {"os":"win32","arch":"any"} (current:{"os":"linux","arch":"x64"})
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: 7zip-bin-mac@1.0.1 (node_modules/7zip-bin-mac):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for 7zip-bin-mac@1.0.1: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.1.3 (node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.1.3: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})

removed 140 packages in 47.473s
sosun@poscoict:~/Desktop/demo/second$ npm run build

> second@1.0.0 build /home/sosun/Desktop/demo/second
> concurrently "npm run build-main" "npm run build-renderer"

[0]
[0] > second@1.0.0 build-main /home/sosun/Desktop/demo/second
[0] > cross-env NODE_ENV=production node --trace-warnings -r babel-register ./node_modules/webpack/bin/webpack --config webpack.config.main.prod.js --colors
[0]
[1]
[1] > second@1.0.0 build-renderer /home/sosun/Desktop/demo/second
[1] > cross-env NODE_ENV=production node --trace-warnings -r babel-register ./node_modules/webpack/bin/webpack --config webpack.config.renderer.prod.js --colors
[1]
[1] 찍혀라[CheckNodeEnv] production
[1] 찍혀라[CheckNodeEnv] production
[0] 찍혀라[CheckNodeEnv] production
[0] 찍혀라[CheckNodeEnv] production
[0] Hash: 431b7e4e42adda27500e
[0] Version: webpack 3.10.0
[0] Time: 5471ms
[0]                  Asset     Size  Chunks             Chunk Names
[0]     ./app/main.prod.js  93.3 kB       0  [emitted]  main
[0] ./app/main.prod.js.map   414 kB       0  [emitted]  main
[0] [./app/main.dev.js] ./app/main.dev.js 3.69 kB {0} [built]
[0] [./app/menu.js] ./app/menu.js 6.48 kB {0} [built]
[0]     + 44 hidden modules
[0] npm run build-main exited with code 0
[1] Hash: 07dc940c9f82200fe6a3
[1] Version: webpack 3.10.0
[1] Time: 24934ms
[1]                                  Asset      Size  Chunks                    Chunk Names
[1]   674f50d287a8c48dc19ba404d20fe713.eot    166 kB          [emitted]
[1]   912ec66d7572ff821749319396470bde.svg    444 kB          [emitted]  [big]
[1]   b06871f281fee6b241d60582ae9369b9.ttf    166 kB          [emitted]
[1] af7ae505a9eed503f8b8e6982036873e.woff2   77.2 kB          [emitted]
[1]  fee66e712a8a08eef5805a46892932ad.woff     98 kB          [emitted]
[1]                       renderer.prod.js    458 kB       0  [emitted]  [big]  main
[1]                              style.css   31.7 kB       0  [emitted]         main
[1]                   renderer.prod.js.map   1.31 MB       0  [emitted]         main
[1]                          style.css.map  86 bytes       0  [emitted]         main
[1] [./app/app.global.css] ./app/app.global.css 41 bytes {0} [built]
[1] [./app/containers/App.js] ./app/containers/App.js 1.81 kB {0} [built]
[1] [./app/containers/CameraPage.js] ./app/containers/CameraPage.js 1.62 kB {0} [built]
[1] [./app/containers/FilesPage.js] ./app/containers/FilesPage.js 1.61 kB {0} [built]
[1] [./app/containers/HomePage.js] ./app/containers/HomePage.js 2.21 kB {0} [built]
[1] [./app/containers/LoginPage.js] ./app/containers/LoginPage.js 912 bytes {0} [built]
[1] [./app/containers/MenuPage.js] ./app/containers/MenuPage.js 1.46 kB {0} [built]
[1] [./app/containers/Root.js] ./app/containers/Root.js 3.13 kB {0} [built]
[1] [./app/containers/SettingsPage.js] ./app/containers/SettingsPage.js 1.63 kB {0} [built]
[1] [./app/index.js] ./app/index.js 4.61 kB {0} [built]
[1] [./app/reducers/defaultChecker.js] ./app/reducers/defaultChecker.js 3.13 kB {0} [built]
[1] [./app/store/configureStore.js] ./app/store/configureStore.js 251 bytes {0} [built]
[1] [./app/store/configureStore.prod.js] ./app/store/configureStore.prod.js 897 bytes {0} [built]
[1] [./app/utils/firebase.js] ./app/utils/firebase.js 947 bytes {0} [built]
[1] [./node_modules/css-loader/index.js?{"minimize":true}!./app/app.global.css] ./node_modules/css-loader?{"minimize":true}!./app/app.global.css 698 bytes [built]
[1]     + 279 hidden modules
[1] Child extract-text-webpack-plugin node_modules/extract-text-webpack-plugin/dist node_modules/css-loader/index.js??ref--2-1!app/components/Mymenu.css:
[1]        2 modules
[1] Child extract-text-webpack-plugin node_modules/extract-text-webpack-plugin/dist node_modules/css-loader/index.js??ref--2-1!app/components/Home.css:
[1]        2 modules
[1] Child extract-text-webpack-plugin node_modules/extract-text-webpack-plugin/dist node_modules/css-loader/index.js??ref--1-2!app/app.global.css:
[1]      5 assets
[1]     [./node_modules/css-loader/index.js?{"minimize":true}!./app/app.global.css] ./node_modules/css-loader?{"minimize":true}!./app/app.global.css 698 bytes {0} [built]
[1]         + 9 hidden modules
[1] npm run build-renderer exited with code 0
sosun@poscoict:~/Desktop/demo/second$ npm run dev

> second@1.0.0 dev /home/sosun/Desktop/demo/second
> cross-env START_HOT=1 node -r babel-register ./internals/scripts/CheckPortInUse.js && cross-env START_HOT=1 npm run start-renderer-dev

찍혀라[CheckPortInUse]
찍혀라[CheckPortInUse] 1212 undefined
찍혀라[CheckPortInUse] cross-env PORT=1212 를 사용할 수도 있을듯

> second@1.0.0 start-renderer-dev /home/sosun/Desktop/demo/second
> cross-env NODE_ENV=development node --trace-warnings -r babel-register ./node_modules/webpack-dev-server/bin/webpack-dev-server --config webpack.config.renderer.dev.js

찍혀라[webpack.config.render.dev] call CheckNodeEnv
찍혀라[CheckNodeEnv] development
찍혀라[CheckNodeEnv] development
찍혀라[webpack.config.render.dev] DLL 빌드여부 확인
찍혀라[webpack.config.render.dev] /home/sosun/Desktop/demo/second/dll /home/sosun/Desktop/demo/second/dll/renderer.json
찍혀라[webpack.config.render.dev] START_HOT 환경변수: 1
Starting Main Process...
찍혀라[webpack.config.render.dev] child_process를 생성함.
Project is running at http://localhost:1212/
webpack output is served from http://localhost:1212/dist
Content not from webpack is served from /home/sosun/Desktop/demo/second/dist
404s will fallback to /index.html

> second@1.0.0 start-main-dev /home/sosun/Desktop/demo/second
> cross-env HOT=1 NODE_ENV=development electron -r babel-register ./app/main.dev

찍혀라[main.dev] development
찍혀라[main.dev] 뭘 설치하나벼
찍혀라[main.dev] ready 되면 BrowserWindow 생성해야지
찍혀라[main.dev] /home/sosun/Desktop/demo/second/app
찍혀라[main.dev] 로딩이 되어나벼
```

#### after-merge
origin-master에 업데이트 된 내용을 merge 하고 다시 uninstall firebase 실행. 그리고 아예 새 파일이니까 다시 처음부터 npm install 해쥼.

...

$ npm install

flow-type 에서 dependency 에러 한 번 내주고, childProcess 어쩌고 에러 냄..^^

```s
sosun@poscoict:~/Desktop/demo/second$ npm uninstall firebase
npm WARN postcss-html@0.12.0 requires a peer of postcss-less@>=1.1.0 but none is installed. You must install peer dependencies yourself.
npm WARN postcss-html@0.12.0 requires a peer of sugarss@>=1.0.0 but none is installed. You must install peer dependencies yourself.
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: 7zip-bin-win@2.1.1 (node_modules/7zip-bin-win):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for 7zip-bin-win@2.1.1: wanted {"os":"win32","arch":"any"} (current:{"os":"linux","arch":"x64"})
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: 7zip-bin-mac@1.0.1 (node_modules/7zip-bin-mac):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for 7zip-bin-mac@1.0.1: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.1.3 (node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.1.3: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})

up to date in 48.819s
sosun@poscoict:~/Desktop/demo/second$ npm install

> second@1.0.0 postinstall /home/sosun/Desktop/demo/second
> node -r babel-register internals/scripts/CheckNativeDep.js && npm run flow-typed && npm run build-dll && electron-builder install-app-deps && node node_modules/fbjs-scripts/node/check-dev-engines.js package.json

찍혀라[CheckNativeDep] ./package.json 파일의 dependecies 부분 { devtron: '^1.4.0',
  'electron-debug': '^1.5.0',
  'font-awesome': '^4.7.0',
  history: '^4.7.2',
  react: '^16.2.0',
  'react-desktop': '^0.3.3',
  'react-dom': '^16.2.0',
  'react-hot-loader': '^4.0.0-beta.13',
  'react-redux': '^5.0.6',
  'react-router': '^4.2.0',
  'react-router-dom': '^4.2.2',
  'react-router-redux': '^5.0.0-alpha.6',
  redux: '^3.7.2',
  'redux-thunk': '^2.2.0',
  'source-map-support': '^0.5.0' }
찍혀라[CheckNativeDep] { name: 'second',
  version: '1.0.0',
  dependencies:
   { 'node-sass':
      { version: '4.7.2',
        from: 'node-sass@^4.7.2',
        resolved: 'https://registry.npmjs.org/node-sass/-/node-sass-4.7.2.tgz' } } }
찍혀라[CheckNativeDep] 0

> second@1.0.0 flow-typed /home/sosun/Desktop/demo/second
> rimraf flow-typed/npm && flow-typed install --overwrite || true

• Found 84 dependencies in package.json to install libdefs for. Searching...
• rebasing flow-typed cache...
• Installing 12 libDefs...
  • jest_v22.x.x.js
    └> ./flow-typed/npm/jest_v22.x.x.js
jest
/home/sosun/Desktop/demo/second/flow-typed/npm
  • chalk_v2.x.x.js
    └> ./flow-typed/npm/chalk_v2.x.x.js
chalk
/home/sosun/Desktop/demo/second/flow-typed/npm
  • react-redux_v5.x.x.js
    └> ./flow-typed/npm/react-redux_v5.x.x.js
react-redux
/home/sosun/Desktop/demo/second/flow-typed/npm
  • react-router_v4.x.x.js
    └> ./flow-typed/npm/react-router_v4.x.x.js
react-router
/home/sosun/Desktop/demo/second/flow-typed/npm
  • flow-bin_v0.x.x.js
    └> ./flow-typed/npm/flow-bin_v0.x.x.js
flow-bin
/home/sosun/Desktop/demo/second/flow-typed/npm
  • minimist_v1.x.x.js
    └> ./flow-typed/npm/minimist_v1.x.x.js
minimist
/home/sosun/Desktop/demo/second/flow-typed/npm
  • react-router-dom_v4.x.x.js
    └> ./flow-typed/npm/react-router-dom_v4.x.x.js
react-router-dom
/home/sosun/Desktop/demo/second/flow-typed/npm
  • enzyme_v3.x.x.js
    └> ./flow-typed/npm/enzyme_v3.x.x.js
enzyme
/home/sosun/Desktop/demo/second/flow-typed/npm
  • express_v4.16.x.js
    └> ./flow-typed/npm/express_v4.16.x.js
express
/home/sosun/Desktop/demo/second/flow-typed/npm
  • react-test-renderer_v16.x.x.js
    └> ./flow-typed/npm/react-test-renderer_v16.x.x.js
react-test-renderer
/home/sosun/Desktop/demo/second/flow-typed/npm
  • redux_v3.x.x.js
    └> ./flow-typed/npm/redux_v3.x.x.js
redux
/home/sosun/Desktop/demo/second/flow-typed/npm
  • rimraf_v2.x.x.js
    └> ./flow-typed/npm/rimraf_v2.x.x.js
rimraf
/home/sosun/Desktop/demo/second/flow-typed/npm
• Generating stubs for untyped dependencies...
  • babel-plugin-dev-expression@^0.2.1
    └> flow-typed/npm/babel-plugin-dev-expression_vx.x.x.js
  • npm-logical-tree@^1.2.0
    └> flow-typed/npm/npm-logical-tree_vx.x.x.js
  • stylelint-config-standard@^18.0.0
    └> flow-typed/npm/stylelint-config-standard_vx.x.x.js
  • eslint-formatter-pretty@^1.3.0
    └> flow-typed/npm/eslint-formatter-pretty_vx.x.x.js
  • eslint-import-resolver-webpack@^0.8.4
    └> flow-typed/npm/eslint-import-resolver-webpack_vx.x.x.js
  • electron-debug@^1.5.0
    └> flow-typed/npm/electron-debug_vx.x.x.js
  • url-loader@^0.6.2
    └> flow-typed/npm/url-loader_vx.x.x.js
  • enzyme-to-json@^3.3.0
    └> flow-typed/npm/enzyme-to-json_vx.x.x.js
  • source-map-support@^0.5.0
    └> flow-typed/npm/source-map-support_vx.x.x.js
  • redux-thunk@^2.2.0
    └> flow-typed/npm/redux-thunk_vx.x.x.js
  • react-router-redux@^5.0.0-alpha.6
    └> flow-typed/npm/react-router-redux_vx.x.x.js
  • babel-jest@^22.0.4
    └> flow-typed/npm/babel-jest_vx.x.x.js
  • babel-plugin-dynamic-import-webpack@^1.0.2
    └> flow-typed/npm/babel-plugin-dynamic-import-webpack_vx.x.x.js
  • font-awesome@^4.7.0
    └> flow-typed/npm/font-awesome_vx.x.x.js
  • babel-preset-react@^6.24.1
    └> flow-typed/npm/babel-preset-react_vx.x.x.js
  • babel-plugin-add-module-exports@^0.2.1
    └> flow-typed/npm/babel-plugin-add-module-exports_vx.x.x.js
  • babel-preset-react-optimize@^1.0.1
    └> flow-typed/npm/babel-preset-react-optimize_vx.x.x.js
  • babel-preset-stage-0@^6.24.1
    └> flow-typed/npm/babel-preset-stage-0_vx.x.x.js
  • detect-port@^1.2.2
    └> flow-typed/npm/detect-port_vx.x.x.js
  • babel-preset-react-hmre@^1.1.1
    └> flow-typed/npm/babel-preset-react-hmre_vx.x.x.js
  • electron-devtools-installer@^2.2.3
    └> flow-typed/npm/electron-devtools-installer_vx.x.x.js
  • babel-register@^6.26.0
    └> flow-typed/npm/babel-register_vx.x.x.js
  • eslint-config-airbnb@^16.1.0
    └> flow-typed/npm/eslint-config-airbnb_vx.x.x.js
  • enzyme-adapter-react-16@^1.1.1
    └> flow-typed/npm/enzyme-adapter-react-16_vx.x.x.js
  • file-loader@^1.1.6
    └> flow-typed/npm/file-loader_vx.x.x.js
  • babel-preset-env@^1.6.1
    └> flow-typed/npm/babel-preset-env_vx.x.x.js
  • redux-logger@^3.0.6
    └> flow-typed/npm/redux-logger_vx.x.x.js
  • sass-loader@^6.0.6
    └> flow-typed/npm/sass-loader_vx.x.x.js
  • spectron@^3.7.2
    └> flow-typed/npm/spectron_vx.x.x.js
  • stylefmt@^6.0.0
    └> flow-typed/npm/stylefmt_vx.x.x.js
  • style-loader@^0.19.1
    └> flow-typed/npm/style-loader_vx.x.x.js
  • babel-plugin-transform-class-properties@^6.24.1
    └> flow-typed/npm/babel-plugin-transform-class-properties_vx.x.x.js
  • webpack-merge@^4.1.1
    └> flow-typed/npm/webpack-merge_vx.x.x.js
  • history@^4.7.2
    └> flow-typed/npm/history_vx.x.x.js
  • babel-loader@^7.1.2
    └> flow-typed/npm/babel-loader_vx.x.x.js
  • cross-env@^5.1.3
    └> flow-typed/npm/cross-env_vx.x.x.js
  • babel-eslint@^8.2.0
    └> flow-typed/npm/babel-eslint_vx.x.x.js
  • concurrently@^3.5.1
    └> flow-typed/npm/concurrently_vx.x.x.js
  • electron-builder@^19.55.0
    └> flow-typed/npm/electron-builder_vx.x.x.js
  • electron@^1.7.10
    └> flow-typed/npm/electron_vx.x.x.js
  • css-loader@^0.28.8
    └> flow-typed/npm/css-loader_vx.x.x.js
  • babel-plugin-transform-es2015-classes@^6.24.1
    └> flow-typed/npm/babel-plugin-transform-es2015-classes_vx.x.x.js
  • eslint-plugin-promise@^3.6.0
    └> flow-typed/npm/eslint-plugin-promise_vx.x.x.js
  • extract-text-webpack-plugin@^3.0.2
    └> flow-typed/npm/extract-text-webpack-plugin_vx.x.x.js
  • fbjs-scripts@^0.8.1
    └> flow-typed/npm/fbjs-scripts_vx.x.x.js
  • eslint-plugin-import@^2.8.0
    └> flow-typed/npm/eslint-plugin-import_vx.x.x.js
  • identity-obj-proxy@^3.0.0
    └> flow-typed/npm/identity-obj-proxy_vx.x.x.js
  • uglifyjs-webpack-plugin@1.1.6
    └> flow-typed/npm/uglifyjs-webpack-plugin_vx.x.x.js
  • eslint-plugin-react@^7.5.1
    └> flow-typed/npm/eslint-plugin-react_vx.x.x.js
  • webpack-dev-server@^2.10.0
    └> flow-typed/npm/webpack-dev-server_vx.x.x.js
  • webpack-bundle-analyzer@^2.9.2
    └> flow-typed/npm/webpack-bundle-analyzer_vx.x.x.js
  • cross-spawn@^5.1.0
    └> flow-typed/npm/cross-spawn_vx.x.x.js
  • eslint-plugin-compat@^2.1.0
    └> flow-typed/npm/eslint-plugin-compat_vx.x.x.js
  • webpack@^3.10.0
    └> flow-typed/npm/webpack_vx.x.x.js
  • devtron@^1.4.0
    └> flow-typed/npm/devtron_vx.x.x.js
  • react-hot-loader@^4.0.0-beta.13
    └> flow-typed/npm/react-hot-loader_vx.x.x.js
  • eslint@^4.15.0
    └> flow-typed/npm/eslint_vx.x.x.js
  • eslint-plugin-flowtype@^2.41.0
    └> flow-typed/npm/eslint-plugin-flowtype_vx.x.x.js
  • electron-rebuild@^1.6.0
    └> flow-typed/npm/electron-rebuild_vx.x.x.js
  • eslint-plugin-jest@^21.5.0
    └> flow-typed/npm/eslint-plugin-jest_vx.x.x.js
  • flow-typed@^2.2.3
    └> flow-typed/npm/flow-typed_vx.x.x.js
  • stylelint@^8.4.0
    └> flow-typed/npm/stylelint_vx.x.x.js
  • babel-core@^6.26.0
    └> flow-typed/npm/babel-core_vx.x.x.js
  • eslint-plugin-jsx-a11y@6.0.3
    └> flow-typed/npm/eslint-plugin-jsx-a11y_vx.x.x.js
  • flow-runtime@^0.16.0
    └> flow-typed/npm/flow-runtime_vx.x.x.js
  • sinon@^4.1.4
    └> flow-typed/npm/sinon_vx.x.x.js
  • node-sass@^4.7.2
    └> flow-typed/npm/node-sass_vx.x.x.js
  • babel-plugin-flow-runtime@^0.15.0
    └> flow-typed/npm/babel-plugin-flow-runtime_vx.x.x.js
  • react-desktop@^0.3.3
    └> flow-typed/npm/react-desktop_vx.x.x.js
  • jsdom@^11.5.1
    └> flow-typed/npm/jsdom_vx.x.x.js

!! No flow@v0.63.1-compatible libdefs found in flow-typed for the above untyped dependencies !!

I've generated `any`-typed stubs for these packages, but consider submitting
libdefs for them to https://github.com/flowtype/flow-typed/


> second@1.0.0 build-dll /home/sosun/Desktop/demo/second
> cross-env NODE_ENV=development node --trace-warnings -r babel-register ./node_modules/webpack/bin/webpack --config webpack.config.renderer.dev.dll.js --colors

찍혀라[webpack.config.render.dev.dll] call CheckNodeEnv
찍혀라[CheckNodeEnv] development
찍혀라[CheckNodeEnv] development
찍혀라[webpack.config.render.dev.dll] /home/sosun/Desktop/demo/second/dll
Hash: 0c64b3e5b6c61b48b5fe
Version: webpack 3.10.0
Time: 3921ms
              Asset     Size  Chunks                    Chunk Names
renderer.dev.dll.js  1.89 MB       0  [emitted]  [big]  renderer
[./node_modules/electron-debug recursive] ./node_modules/electron-debug 160 bytes {0} [built]
[./node_modules/webpack/buildin/amd-define.js] (webpack)/buildin/amd-define.js 88 bytes {0} [built]
[./node_modules/webpack/buildin/module.js] (webpack)/buildin/module.js 517 bytes {0} [built]
   [0] dll renderer 12 bytes {0} [built]
    + 333 hidden modules

WARNING in ./node_modules/electron-debug/index.js
81:45-58 Critical dependency: the request of a dependency is an expression
 @ ./node_modules/electron-debug/index.js
 @ dll renderer

WARNING in ./node_modules/electron-debug/index.js
84:85-106 Critical dependency: the request of a dependency is an expression
 @ ./node_modules/electron-debug/index.js
 @ dll renderer
  • electron-builder version=19.55.2
  • loaded configuration file=package.json ("build" field)
  • installing production dependencies platform=linux arch=x64 appDir=/home/sosun/Desktop/demo/second/app
Error: /usr/bin/node exited with code 1
Output:

> grpc@1.8.4 install /home/sosun/Desktop/demo/second/app/node_modules/grpc
> node-pre-gyp install --fallback-to-build --library=static_library


Error output:
sh: 1: node-pre-gyp: not found
npm WARN second@1.0.0 No repository field.

npm ERR! file sh
npm ERR! code ELIFECYCLE
npm ERR! errno ENOENT
npm ERR! syscall spawn
npm ERR! grpc@1.8.4 install: `node-pre-gyp install --fallback-to-build --library=static_library`
npm ERR! spawn ENOENT
npm ERR!
npm ERR! Failed at the grpc@1.8.4 install script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     /home/sosun/.npm/_logs/2018-01-25T09_20_51_146Z-debug.log

    at ChildProcess.childProcess.once.code (/home/sosun/Desktop/demo/second/node_modules/builder-util/src/util.ts:241:14)
    at Object.onceWrapper (events.js:317:30)
    at emitTwo (events.js:126:13)
    at ChildProcess.emit (events.js:214:7)
    at maybeClose (internal/child_process.js:925:16)
    at Socket.stream.socket.on (internal/child_process.js:346:11)
    at emitOne (events.js:116:13)
    at Socket.emit (events.js:211:7)
    at Pipe._handle.close [as _onclose] (net.js:554:12)
From previous event:
    at spawn (/home/sosun/Desktop/demo/second/node_modules/builder-util/src/util.ts:200:3)
    at installDependencies (/home/sosun/Desktop/demo/second/node_modules/electron-builder-lib/src/util/yarn.ts:87:3)
    at /home/sosun/Desktop/demo/second/node_modules/electron-builder-lib/src/util/yarn.ts:17:11
    at Generator.next (<anonymous>)
From previous event:
    at installOrRebuild (/home/sosun/Desktop/demo/second/node_modules/electron-builder-lib/out/util/yarn.js:31:21)
    at /home/sosun/Desktop/demo/second/node_modules/electron-builder/src/cli/install-app-deps.ts:58:42
    at Generator.next (<anonymous>)
From previous event:
    at installAppDeps (/home/sosun/Desktop/demo/second/node_modules/electron-builder/out/cli/install-app-deps.js:51:21)
    at then (/home/sosun/Desktop/demo/second/node_modules/electron-builder/src/cli/cli.ts:48:33)
    at runCallback (timers.js:789:20)
    at tryOnImmediate (timers.js:751:5)
    at processImmediate [as _immediateCallback] (timers.js:722:5)
From previous event:
    at Object.args [as handler] (/home/sosun/Desktop/demo/second/node_modules/electron-builder/src/cli/cli.ts:48:33)
    at Object.runCommand (/home/sosun/Desktop/demo/second/node_modules/electron-builder/node_modules/yargs/lib/command.js:235:44)
    at Object.parseArgs [as _parseArgs] (/home/sosun/Desktop/demo/second/node_modules/electron-builder/node_modules/yargs/yargs.js:1013:30)
    at Object.get [as argv] (/home/sosun/Desktop/demo/second/node_modules/electron-builder/node_modules/yargs/yargs.js:957:21)
    at Object.<anonymous> (/home/sosun/Desktop/demo/second/node_modules/electron-builder/src/cli/cli.ts:42:15)
    at Module._compile (module.js:643:30)
    at Object.Module._extensions..js (module.js:654:10)
    at Module.load (module.js:556:32)
    at tryModuleLoad (module.js:499:12)
    at Function.Module._load (module.js:491:3)
    at Function.Module.runMain (module.js:684:10)
    at startup (bootstrap_node.js:187:16)
    at bootstrap_node.js:608:3
npm ERR! code ELIFECYCLE
npm ERR! errno 1
npm ERR! second@1.0.0 postinstall: `node -r babel-register internals/scripts/CheckNativeDep.js && npm run flow-typed && npm run build-dll && electron-builder install-app-deps && node node_modules/fbjs-scripts/node/check-dev-engines.js package.json`
npm ERR! Exit status 1
npm ERR!
npm ERR! Failed at the second@1.0.0 postinstall script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     /home/sosun/.npm/_logs/2018-01-25T09_20_51_410Z-debug.log
```



#### npm install build && npm install dev

npm install 에서 수많은 에러가 났지만, npm run build를 일단 해봄.
잘 된다...

$ npm run build

$ npm run dev

```s
sosun@poscoict:~/Desktop/demo/second$ npm run build

> second@1.0.0 build /home/sosun/Desktop/demo/second
> concurrently "npm run build-main" "npm run build-renderer"

[0]
[0] > second@1.0.0 build-main /home/sosun/Desktop/demo/second
[0] > cross-env NODE_ENV=production node --trace-warnings -r babel-register ./node_modules/webpack/bin/webpack --config webpack.config.main.prod.js --colors
[0]
[1]
[1] > second@1.0.0 build-renderer /home/sosun/Desktop/demo/second
[1] > cross-env NODE_ENV=production node --trace-warnings -r babel-register ./node_modules/webpack/bin/webpack --config webpack.config.renderer.prod.js --colors
[1]
[1] 찍혀라[CheckNodeEnv] production
[1] 찍혀라[CheckNodeEnv] production
[0] 찍혀라[CheckNodeEnv] production
[0] 찍혀라[CheckNodeEnv] production
[0] Hash: 431b7e4e42adda27500e
[0] Version: webpack 3.10.0
[0] Time: 5243ms
[0]                  Asset     Size  Chunks             Chunk Names
[0]     ./app/main.prod.js  93.3 kB       0  [emitted]  main
[0] ./app/main.prod.js.map   414 kB       0  [emitted]  main
[0] [./app/main.dev.js] ./app/main.dev.js 3.69 kB {0} [built]
[0] [./app/menu.js] ./app/menu.js 6.48 kB {0} [built]
[0]     + 44 hidden modules
[0] npm run build-main exited with code 0
[1] Hash: 07dc940c9f82200fe6a3
[1] Version: webpack 3.10.0
[1] Time: 23367ms
[1]                                  Asset      Size  Chunks                    Chunk Names
[1]   674f50d287a8c48dc19ba404d20fe713.eot    166 kB          [emitted]
[1]   912ec66d7572ff821749319396470bde.svg    444 kB          [emitted]  [big]
[1]   b06871f281fee6b241d60582ae9369b9.ttf    166 kB          [emitted]
[1] af7ae505a9eed503f8b8e6982036873e.woff2   77.2 kB          [emitted]
[1]  fee66e712a8a08eef5805a46892932ad.woff     98 kB          [emitted]
[1]                       renderer.prod.js    458 kB       0  [emitted]  [big]  main
[1]                              style.css   31.7 kB       0  [emitted]         main
[1]                   renderer.prod.js.map   1.31 MB       0  [emitted]         main
[1]                          style.css.map  86 bytes       0  [emitted]         main
[1] [./app/app.global.css] ./app/app.global.css 41 bytes {0} [built]
[1] [./app/containers/App.js] ./app/containers/App.js 1.81 kB {0} [built]
[1] [./app/containers/CameraPage.js] ./app/containers/CameraPage.js 1.62 kB {0} [built]
[1] [./app/containers/FilesPage.js] ./app/containers/FilesPage.js 1.61 kB {0} [built]
[1] [./app/containers/HomePage.js] ./app/containers/HomePage.js 2.21 kB {0} [built]
[1] [./app/containers/LoginPage.js] ./app/containers/LoginPage.js 912 bytes {0} [built]
[1] [./app/containers/MenuPage.js] ./app/containers/MenuPage.js 1.46 kB {0} [built]
[1] [./app/containers/Root.js] ./app/containers/Root.js 3.13 kB {0} [built]
[1] [./app/containers/SettingsPage.js] ./app/containers/SettingsPage.js 1.63 kB {0} [built]
[1] [./app/index.js] ./app/index.js 4.61 kB {0} [built]
[1] [./app/reducers/defaultChecker.js] ./app/reducers/defaultChecker.js 3.13 kB {0} [built]
[1] [./app/store/configureStore.js] ./app/store/configureStore.js 251 bytes {0} [built]
[1] [./app/store/configureStore.prod.js] ./app/store/configureStore.prod.js 897 bytes {0} [built]
[1] [./app/utils/firebase.js] ./app/utils/firebase.js 947 bytes {0} [built]
[1] [./node_modules/css-loader/index.js?{"minimize":true}!./app/app.global.css] ./node_modules/css-loader?{"minimize":true}!./app/app.global.css 698 bytes [built]
[1]     + 279 hidden modules
[1] Child extract-text-webpack-plugin node_modules/extract-text-webpack-plugin/dist node_modules/css-loader/index.js??ref--2-1!app/components/Mymenu.css:
[1]        2 modules
[1] Child extract-text-webpack-plugin node_modules/extract-text-webpack-plugin/dist node_modules/css-loader/index.js??ref--2-1!app/components/Home.css:
[1]        2 modules
[1] Child extract-text-webpack-plugin node_modules/extract-text-webpack-plugin/dist node_modules/css-loader/index.js??ref--1-2!app/app.global.css:
[1]      5 assets
[1]     [./node_modules/css-loader/index.js?{"minimize":true}!./app/app.global.css] ./node_modules/css-loader?{"minimize":true}!./app/app.global.css 698 bytes {0} [built]
[1]         + 9 hidden modules
[1] npm run build-renderer exited with code 0



sosun@poscoict:~/Desktop/demo/second$ npm run dev

> second@1.0.0 dev /home/sosun/Desktop/demo/second
> cross-env START_HOT=1 node -r babel-register ./internals/scripts/CheckPortInUse.js && cross-env START_HOT=1 npm run start-renderer-dev

찍혀라[CheckPortInUse]
찍혀라[CheckPortInUse] 1212 undefined
찍혀라[CheckPortInUse] cross-env PORT=1212 를 사용할 수도 있을듯

> second@1.0.0 start-renderer-dev /home/sosun/Desktop/demo/second
> cross-env NODE_ENV=development node --trace-warnings -r babel-register ./node_modules/webpack-dev-server/bin/webpack-dev-server --config webpack.config.renderer.dev.js

찍혀라[webpack.config.render.dev] call CheckNodeEnv
찍혀라[CheckNodeEnv] development
찍혀라[CheckNodeEnv] development
찍혀라[webpack.config.render.dev] DLL 빌드여부 확인
찍혀라[webpack.config.render.dev] /home/sosun/Desktop/demo/second/dll /home/sosun/Desktop/demo/second/dll/renderer.json
찍혀라[webpack.config.render.dev] START_HOT 환경변수: 1
Starting Main Process...
찍혀라[webpack.config.render.dev] child_process를 생성함.
Project is running at http://localhost:1212/
webpack output is served from http://localhost:1212/dist
Content not from webpack is served from /home/sosun/Desktop/demo/second/dist
404s will fallback to /index.html

> second@1.0.0 start-main-dev /home/sosun/Desktop/demo/second
> cross-env HOT=1 NODE_ENV=development electron -r babel-register ./app/main.dev

찍혀라[main.dev] development
찍혀라[main.dev] 뭘 설치하나벼
찍혀라[main.dev] ready 되면 BrowserWindow 생성해야지
찍혀라[main.dev] /home/sosun/Desktop/demo/second/app
찍혀라[main.dev] 로딩이 되어나벼
sosun@poscoict:~/Desktop/demo/second$ cd app
sosun@poscoict:~/Desktop/demo/second/app$ npm install firebase --save

> grpc@1.8.4 install /home/sosun/Desktop/demo/second/app/node_modules/grpc
> node-pre-gyp install --fallback-to-build --library=static_library

[grpc] Success: "/home/sosun/Desktop/demo/second/app/node_modules/grpc/src/node/extension_binary/node-v57-linux-x64-glibc/grpc_node.node" is installedvia remote
npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN second@1.0.0 No repository field.

+ firebase@4.9.0
added 152 packages in 13.643s
sosun@poscoict:~/Desktop/demo/second/app$ cd ..
sosun@poscoict:~/Desktop/demo/second$ npm run dev

> second@1.0.0 dev /home/sosun/Desktop/demo/second
> cross-env START_HOT=1 node -r babel-register ./internals/scripts/CheckPortInUse.js && cross-env START_HOT=1 npm run start-renderer-dev

찍혀라[CheckPortInUse]
찍혀라[CheckPortInUse] 1212 undefined
찍혀라[CheckPortInUse] cross-env PORT=1212 를 사용할 수도 있을듯

> second@1.0.0 start-renderer-dev /home/sosun/Desktop/demo/second
> cross-env NODE_ENV=development node --trace-warnings -r babel-register ./node_modules/webpack-dev-server/bin/webpack-dev-server --config webpack.config.renderer.dev.js

찍혀라[webpack.config.render.dev] call CheckNodeEnv
찍혀라[CheckNodeEnv] development
찍혀라[CheckNodeEnv] development
찍혀라[webpack.config.render.dev] DLL 빌드여부 확인
찍혀라[webpack.config.render.dev] /home/sosun/Desktop/demo/second/dll /home/sosun/Desktop/demo/second/dll/renderer.json
찍혀라[webpack.config.render.dev] START_HOT 환경변수: 1
Starting Main Process...
찍혀라[webpack.config.render.dev] child_process를 생성함.
Project is running at http://localhost:1212/
webpack output is served from http://localhost:1212/dist
Content not from webpack is served from /home/sosun/Desktop/demo/second/dist
404s will fallback to /index.html

> second@1.0.0 start-main-dev /home/sosun/Desktop/demo/second
> cross-env HOT=1 NODE_ENV=development electron -r babel-register ./app/main.dev

찍혀라[main.dev] development
찍혀라[main.dev] 뭘 설치하나벼
찍혀라[main.dev] ready 되면 BrowserWindow 생성해야지
찍혀라[main.dev] /home/sosun/Desktop/demo/second/app
찍혀라[main.dev] 로딩이 되어나벼
sosun@poscoict:~/Desktop/demo/second$ npm install

> second@1.0.0 postinstall /home/sosun/Desktop/demo/second
> node -r babel-register internals/scripts/CheckNativeDep.js && npm run flow-typed && npm run build-dll && electron-builder install-app-deps && node node_modules/fbjs-scripts/node/check-dev-engines.js package.json

찍혀라[CheckNativeDep] ./package.json 파일의 dependecies 부분 { devtron: '^1.4.0',
  'electron-debug': '^1.5.0',
  'font-awesome': '^4.7.0',
  history: '^4.7.2',
  react: '^16.2.0',
  'react-desktop': '^0.3.3',
  'react-dom': '^16.2.0',
  'react-hot-loader': '^4.0.0-beta.13',
  'react-redux': '^5.0.6',
  'react-router': '^4.2.0',
  'react-router-dom': '^4.2.2',
  'react-router-redux': '^5.0.0-alpha.6',
  redux: '^3.7.2',
  'redux-thunk': '^2.2.0',
  'source-map-support': '^0.5.0' }
찍혀라[CheckNativeDep] { name: 'second',
  version: '1.0.0',
  dependencies:
   { 'node-sass':
      { version: '4.7.2',
        from: 'node-sass@^4.7.2',
        resolved: 'https://registry.npmjs.org/node-sass/-/node-sass-4.7.2.tgz' } } }
찍혀라[CheckNativeDep] 0

> second@1.0.0 flow-typed /home/sosun/Desktop/demo/second
> rimraf flow-typed/npm && flow-typed install --overwrite || true

• Found 84 dependencies in package.json to install libdefs for. Searching...
• rebasing flow-typed cache...
• Installing 12 libDefs...
  • minimist_v1.x.x.js
    └> ./flow-typed/npm/minimist_v1.x.x.js
minimist
/home/sosun/Desktop/demo/second/flow-typed/npm
  • redux_v3.x.x.js
    └> ./flow-typed/npm/redux_v3.x.x.js
redux
/home/sosun/Desktop/demo/second/flow-typed/npm
  • react-test-renderer_v16.x.x.js
    └> ./flow-typed/npm/react-test-renderer_v16.x.x.js
react-test-renderer
/home/sosun/Desktop/demo/second/flow-typed/npm
  • react-redux_v5.x.x.js
    └> ./flow-typed/npm/react-redux_v5.x.x.js
react-redux
/home/sosun/Desktop/demo/second/flow-typed/npm
  • rimraf_v2.x.x.js
    └> ./flow-typed/npm/rimraf_v2.x.x.js
rimraf
/home/sosun/Desktop/demo/second/flow-typed/npm
  • react-router-dom_v4.x.x.js
    └> ./flow-typed/npm/react-router-dom_v4.x.x.js
react-router-dom
/home/sosun/Desktop/demo/second/flow-typed/npm
  • jest_v22.x.x.js
    └> ./flow-typed/npm/jest_v22.x.x.js
jest
/home/sosun/Desktop/demo/second/flow-typed/npm
  • enzyme_v3.x.x.js
    └> ./flow-typed/npm/enzyme_v3.x.x.js
enzyme
/home/sosun/Desktop/demo/second/flow-typed/npm
  • express_v4.16.x.js
    └> ./flow-typed/npm/express_v4.16.x.js
express
/home/sosun/Desktop/demo/second/flow-typed/npm
  • flow-bin_v0.x.x.js
    └> ./flow-typed/npm/flow-bin_v0.x.x.js
flow-bin
/home/sosun/Desktop/demo/second/flow-typed/npm
  • chalk_v2.x.x.js
    └> ./flow-typed/npm/chalk_v2.x.x.js
chalk
/home/sosun/Desktop/demo/second/flow-typed/npm
  • react-router_v4.x.x.js
    └> ./flow-typed/npm/react-router_v4.x.x.js
react-router
/home/sosun/Desktop/demo/second/flow-typed/npm
• Generating stubs for untyped dependencies...
  • electron-debug@^1.5.0
    └> flow-typed/npm/electron-debug_vx.x.x.js
  • eslint-import-resolver-webpack@^0.8.4
    └> flow-typed/npm/eslint-import-resolver-webpack_vx.x.x.js
  • url-loader@^0.6.2
    └> flow-typed/npm/url-loader_vx.x.x.js
  • source-map-support@^0.5.0
    └> flow-typed/npm/source-map-support_vx.x.x.js
  • eslint-formatter-pretty@^1.3.0
    └> flow-typed/npm/eslint-formatter-pretty_vx.x.x.js
  • enzyme-to-json@^3.3.0
    └> flow-typed/npm/enzyme-to-json_vx.x.x.js
  • babel-plugin-dev-expression@^0.2.1
    └> flow-typed/npm/babel-plugin-dev-expression_vx.x.x.js
  • stylelint-config-standard@^18.0.0
    └> flow-typed/npm/stylelint-config-standard_vx.x.x.js
  • npm-logical-tree@^1.2.0
    └> flow-typed/npm/npm-logical-tree_vx.x.x.js
  • react-router-redux@^5.0.0-alpha.6
    └> flow-typed/npm/react-router-redux_vx.x.x.js
  • redux-thunk@^2.2.0
    └> flow-typed/npm/redux-thunk_vx.x.x.js
  • babel-plugin-add-module-exports@^0.2.1
    └> flow-typed/npm/babel-plugin-add-module-exports_vx.x.x.js
  • babel-plugin-dynamic-import-webpack@^1.0.2
    └> flow-typed/npm/babel-plugin-dynamic-import-webpack_vx.x.x.js
  • babel-jest@^22.0.4
    └> flow-typed/npm/babel-jest_vx.x.x.js
  • babel-register@^6.26.0
    └> flow-typed/npm/babel-register_vx.x.x.js
  • babel-preset-stage-0@^6.24.1
    └> flow-typed/npm/babel-preset-stage-0_vx.x.x.js
  • babel-preset-env@^1.6.1
    └> flow-typed/npm/babel-preset-env_vx.x.x.js
  • babel-preset-react-optimize@^1.0.1
    └> flow-typed/npm/babel-preset-react-optimize_vx.x.x.js
  • babel-preset-react-hmre@^1.1.1
    └> flow-typed/npm/babel-preset-react-hmre_vx.x.x.js
  • babel-preset-react@^6.24.1
    └> flow-typed/npm/babel-preset-react_vx.x.x.js
  • detect-port@^1.2.2
    └> flow-typed/npm/detect-port_vx.x.x.js
  • electron-devtools-installer@^2.2.3
    └> flow-typed/npm/electron-devtools-installer_vx.x.x.js
  • enzyme-adapter-react-16@^1.1.1
    └> flow-typed/npm/enzyme-adapter-react-16_vx.x.x.js
  • eslint-config-airbnb@^16.1.0
    └> flow-typed/npm/eslint-config-airbnb_vx.x.x.js
  • babel-plugin-transform-class-properties@^6.24.1
    └> flow-typed/npm/babel-plugin-transform-class-properties_vx.x.x.js
  • file-loader@^1.1.6
    └> flow-typed/npm/file-loader_vx.x.x.js
  • font-awesome@^4.7.0
    └> flow-typed/npm/font-awesome_vx.x.x.js
  • sass-loader@^6.0.6
    └> flow-typed/npm/sass-loader_vx.x.x.js
  • redux-logger@^3.0.6
    └> flow-typed/npm/redux-logger_vx.x.x.js
  • stylefmt@^6.0.0
    └> flow-typed/npm/stylefmt_vx.x.x.js
  • style-loader@^0.19.1
    └> flow-typed/npm/style-loader_vx.x.x.js
  • spectron@^3.7.2
    └> flow-typed/npm/spectron_vx.x.x.js
  • webpack-merge@^4.1.1
    └> flow-typed/npm/webpack-merge_vx.x.x.js
  • history@^4.7.2
    └> flow-typed/npm/history_vx.x.x.js
  • babel-loader@^7.1.2
    └> flow-typed/npm/babel-loader_vx.x.x.js
  • concurrently@^3.5.1
    └> flow-typed/npm/concurrently_vx.x.x.js
  • babel-plugin-transform-es2015-classes@^6.24.1
    └> flow-typed/npm/babel-plugin-transform-es2015-classes_vx.x.x.js
  • babel-eslint@^8.2.0
    └> flow-typed/npm/babel-eslint_vx.x.x.js
  • cross-env@^5.1.3
    └> flow-typed/npm/cross-env_vx.x.x.js
  • css-loader@^0.28.8
    └> flow-typed/npm/css-loader_vx.x.x.js
  • electron-builder@^19.55.0
    └> flow-typed/npm/electron-builder_vx.x.x.js
  • electron@^1.7.10
    └> flow-typed/npm/electron_vx.x.x.js
  • eslint-plugin-compat@^2.1.0
    └> flow-typed/npm/eslint-plugin-compat_vx.x.x.js
  • fbjs-scripts@^0.8.1
    └> flow-typed/npm/fbjs-scripts_vx.x.x.js
  • eslint-plugin-react@^7.5.1
    └> flow-typed/npm/eslint-plugin-react_vx.x.x.js
  • eslint-plugin-import@^2.8.0
    └> flow-typed/npm/eslint-plugin-import_vx.x.x.js
  • extract-text-webpack-plugin@^3.0.2
    └> flow-typed/npm/extract-text-webpack-plugin_vx.x.x.js
  • eslint-plugin-promise@^3.6.0
    └> flow-typed/npm/eslint-plugin-promise_vx.x.x.js
  • identity-obj-proxy@^3.0.0
    └> flow-typed/npm/identity-obj-proxy_vx.x.x.js
  • cross-spawn@^5.1.0
    └> flow-typed/npm/cross-spawn_vx.x.x.js
  • uglifyjs-webpack-plugin@1.1.6
    └> flow-typed/npm/uglifyjs-webpack-plugin_vx.x.x.js
  • webpack-bundle-analyzer@^2.9.2
    └> flow-typed/npm/webpack-bundle-analyzer_vx.x.x.js
  • webpack-dev-server@^2.10.0
    └> flow-typed/npm/webpack-dev-server_vx.x.x.js
  • webpack@^3.10.0
    └> flow-typed/npm/webpack_vx.x.x.js
  • react-hot-loader@^4.0.0-beta.13
    └> flow-typed/npm/react-hot-loader_vx.x.x.js
  • electron-rebuild@^1.6.0
    └> flow-typed/npm/electron-rebuild_vx.x.x.js
  • eslint-plugin-flowtype@^2.41.0
    └> flow-typed/npm/eslint-plugin-flowtype_vx.x.x.js
  • eslint-plugin-jest@^21.5.0
    └> flow-typed/npm/eslint-plugin-jest_vx.x.x.js
  • flow-typed@^2.2.3
    └> flow-typed/npm/flow-typed_vx.x.x.js
  • devtron@^1.4.0
    └> flow-typed/npm/devtron_vx.x.x.js
  • stylelint@^8.4.0
    └> flow-typed/npm/stylelint_vx.x.x.js
  • eslint@^4.15.0
    └> flow-typed/npm/eslint_vx.x.x.js
  • flow-runtime@^0.16.0
    └> flow-typed/npm/flow-runtime_vx.x.x.js
  • sinon@^4.1.4
    └> flow-typed/npm/sinon_vx.x.x.js
  • babel-core@^6.26.0
    └> flow-typed/npm/babel-core_vx.x.x.js
  • eslint-plugin-jsx-a11y@6.0.3
    └> flow-typed/npm/eslint-plugin-jsx-a11y_vx.x.x.js
  • jsdom@^11.5.1
    └> flow-typed/npm/jsdom_vx.x.x.js
  • babel-plugin-flow-runtime@^0.15.0
    └> flow-typed/npm/babel-plugin-flow-runtime_vx.x.x.js
  • node-sass@^4.7.2
    └> flow-typed/npm/node-sass_vx.x.x.js
  • react-desktop@^0.3.3
    └> flow-typed/npm/react-desktop_vx.x.x.js

!! No flow@v0.63.1-compatible libdefs found in flow-typed for the above untyped dependencies !!

I've generated `any`-typed stubs for these packages, but consider submitting
libdefs for them to https://github.com/flowtype/flow-typed/


> second@1.0.0 build-dll /home/sosun/Desktop/demo/second
> cross-env NODE_ENV=development node --trace-warnings -r babel-register ./node_modules/webpack/bin/webpack --config webpack.config.renderer.dev.dll.js --colors

찍혀라[webpack.config.render.dev.dll] call CheckNodeEnv
찍혀라[CheckNodeEnv] development
찍혀라[CheckNodeEnv] development
찍혀라[webpack.config.render.dev.dll] /home/sosun/Desktop/demo/second/dll
Hash: 0c64b3e5b6c61b48b5fe
Version: webpack 3.10.0
Time: 4406ms
              Asset     Size  Chunks                    Chunk Names
renderer.dev.dll.js  1.89 MB       0  [emitted]  [big]  renderer
[./node_modules/electron-debug recursive] ./node_modules/electron-debug 160 bytes {0} [built]
[./node_modules/webpack/buildin/amd-define.js] (webpack)/buildin/amd-define.js 88 bytes {0} [built]
[./node_modules/webpack/buildin/module.js] (webpack)/buildin/module.js 517 bytes {0} [built]
   [0] dll renderer 12 bytes {0} [built]
    + 333 hidden modules

WARNING in ./node_modules/electron-debug/index.js
81:45-58 Critical dependency: the request of a dependency is an expression
 @ ./node_modules/electron-debug/index.js
 @ dll renderer

WARNING in ./node_modules/electron-debug/index.js
84:85-106 Critical dependency: the request of a dependency is an expression
 @ ./node_modules/electron-debug/index.js
 @ dll renderer
  • electron-builder version=19.55.2
  • loaded configuration file=package.json ("build" field)
  • installing production dependencies platform=linux arch=x64 appDir=/home/sosun/Desktop/demo/second/app
npm WARN postcss-html@0.12.0 requires a peer of postcss-less@>=1.1.0 but none is installed. You must install peer dependencies yourself.
npm WARN postcss-html@0.12.0 requires a peer of sugarss@>=1.0.0 but none is installed. You must install peer dependencies yourself.
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: 7zip-bin-win@2.1.1 (node_modules/7zip-bin-win):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for 7zip-bin-win@2.1.1: wanted {"os":"win32","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: 7zip-bin-mac@1.0.1 (node_modules/7zip-bin-mac):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for 7zip-bin-mac@1.0.1: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.1.3 (node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.1.3: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})

up to date in 401.146s
```
