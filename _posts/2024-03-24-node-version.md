---
title: "Ошибка с версией Node.js"
layout: post
categories: Development
tags: [node]
share: true
---

Довольно часто в своей практике сталкиваюсь с такой ошибкой, когда запускаю локально сторонний проект:

```bash
$ npm run start

> dom-moving-item@1.0.0 start
> webpack serve --config webpack.dev.js

node:internal/crypto/hash:69
  this[kHandle] = new _Hash(algorithm, xofLen);
                  ^

Error: error:0308010C:digital envelope routines::unsupported
    at new Hash (node:internal/crypto/hash:69:19)
    at Object.createHash (node:crypto:133:10)
    at BulkUpdateDecorator.hashFactory (/home/verda/Netology/Homeworks/Javascript/dom/playground/task/node_modules/webpack/lib/util/createHash.js:155:18)
    at BulkUpdateDecorator.digest (/home/verda/Netology/Homeworks/Javascript/dom/playground/task/node_modules/webpack/lib/util/createHash.js:80:21)
    at /home/verda/Netology/Homeworks/Javascript/dom/playground/task/node_modules/webpack/lib/DefinePlugin.js:595:38
    at _next28 (eval at create (/home/verda/Netology/Homeworks/Javascript/dom/playground/task/node_modules/webpack/node_modules/tapable/lib/HookCodeFactory.js:19:10), <anonymous>:38:1)
    at _next6 (eval at create (/home/verda/Netology/Homeworks/Javascript/dom/playground/task/node_modules/webpack/node_modules/tapable/lib/HookCodeFactory.js:19:10), <anonymous>:97:1)
    at Hook.eval [as call] (eval at create (/home/verda/Netology/Homeworks/Javascript/dom/playground/task/node_modules/webpack/node_modules/tapable/lib/HookCodeFactory.js:19:10), <anonymous>:113:1)
    at Hook.CALL_DELEGATE [as _call] (/home/verda/Netology/Homeworks/Javascript/dom/playground/task/node_modules/webpack/node_modules/tapable/lib/Hook.js:14:14)
    at Compiler.newCompilation (/home/verda/Netology/Homeworks/Javascript/dom/playground/task/node_modules/webpack/lib/Compiler.js:1053:26) {
  opensslErrorStack: [ 'error:03000086:digital envelope routines::initialization error' ],
  library: 'digital envelope routines',
  reason: 'unsupported',
  code: 'ERR_OSSL_EVP_UNSUPPORTED'
}
```

... если посмотреть на _package.json_ проекта - там будет _webpack_:

```js
"devDependencies": {
    "@babel/cli": "^7.15.7",
    "@babel/core": "^7.15.5",
    "@babel/preset-env": "^7.15.6",
    "babel-jest": "^27.2.4",
    "babel-loader": "^8.2.2",
    "clean-webpack-plugin": "^4.0.0",
    "css-loader": "^5.2.7",
    "eslint": "^7.32.0",
    "eslint-config-airbnb-base": "^14.2.1",
    "eslint-plugin-import": "^2.24.2",
    "html-loader": "^1.3.2",
    "html-webpack-plugin": "^4.5.2",
    "jest": "^27.2.4",
    "live-server": "^1.2.1",
    "mini-css-extract-plugin": "^1.6.2",
    "optimize-css-assets-webpack-plugin": "^5.0.8",
    "terser-webpack-plugin": "^5.2.4",
    "webpack": "^5.57.1",
    "webpack-cli": "^4.8.0",
    "webpack-dev-server": "^3.11.2",
    "webpack-merge": "^5.8.0"
},
"dependencies": {
    "core-js": "^3.18.2",
    "push-dir": "^0.4.1"
}
```

... причина ошибки - разные версии Node.js на локальной машине и на машине, на которой велась разработка проекта (хотя в деталях не совсем понимаю, в чем именно заключается разница - в самом прокте); если на локальной машине установлен nvm, можно сначала проверить текущую версию Node:

```bash
$ nvm list
       v14.21.3
       v16.20.2
       v18.19.1
->     v20.10.0
default -> node (-> v20.10.0)
iojs -> N/A (default)
unstable -> N/A (default)
node -> stable (-> v20.10.0) (default)
stable -> 20.10 (-> v20.10.0) (default)
lts/* -> lts/iron (-> N/A)
lts/argon -> v4.9.1 (-> N/A)
lts/boron -> v6.17.1 (-> N/A)
lts/carbon -> v8.17.0 (-> N/A)
lts/dubnium -> v10.24.1 (-> N/A)
lts/erbium -> v12.22.12 (-> N/A)
lts/fermium -> v14.21.3
lts/gallium -> v16.20.2
lts/hydrogen -> v18.19.1
lts/iron -> v20.11.1 (-> N/A)
```

... а затем переключаться между версиями Node.js пока не попаем пальцем в небо:

```bash
$ nvm use 16.20.2
Now using node v16.20.2 (npm v8.19.4)
```

```bash
$ npm run start

> dom-moving-item@1.0.0 start
> webpack serve --config webpack.dev.js

ℹ ｢wds｣: Project is running at http://localhost:8888/
ℹ ｢wds｣: webpack output is served from 
ℹ ｢wds｣: Content not from webpack is served from /dist
ℹ ｢wds｣: 404s will fallback to /index.html
Browserslist: caniuse-lite is outdated. Please run:
  npx browserslist@latest --update-db
  Why you should do it regularly: https://github.com/browserslist/browserslist#browsers-data-updating
ℹ ｢wdm｣: wait until bundle finished: /
(node:15343) [DEP_WEBPACK_COMPILATION_ASSETS] DeprecationWarning: Compilation.assets will be frozen in future, all modifications are deprecated.
BREAKING CHANGE: No more changes should happen to Compilation.assets after sealing the Compilation.
        Do changes to assets earlier, e. g. in Compilation.hooks.processAssets.
        Make sure to select an appropriate stage from Compilation.PROCESS_ASSETS_STAGE_*.
(Use `node --trace-deprecation ...` to show where the warning was created)
ℹ ｢wdm｣: assets by chunk 1.18 MiB (name: main)
  asset main.js 1.18 MiB [emitted] (name: main)
  asset main.css 2.46 KiB [emitted] (name: main)
asset assets/goblin2dbd01ce16c0fa83cb67.png 9.93 KiB [emitted] [immutable] [from: src/img/goblin.png] (auxiliary name: main)
asset ./index.html 391 bytes [emitted]
Entrypoint main 1.18 MiB (9.93 KiB) = main.css 2.46 KiB main.js 1.18 MiB 1 auxiliary asset
runtime modules 29.2 KiB 15 modules
modules by path ./node_modules/core-js/ 52.7 KiB 86 modules
modules by path ./node_modules/webpack-dev-server/ 21.2 KiB
  modules by path ./node_modules/webpack-dev-server/client/ 20.9 KiB 10 modules
  modules by path ./node_modules/webpack-dev-server/node_modules/ 296 bytes 2 modules
modules by path ./src/ 3.74 KiB (javascript) 706 bytes (css/mini-extract) 9.93 KiB (asset) 6 modules
modules by path ./node_modules/html-entities/lib/*.js 61 KiB 5 modules
modules by path ./node_modules/webpack/hot/ 1.58 KiB 3 modules
modules by path ./node_modules/url/ 37.4 KiB 3 modules
modules by path ./node_modules/querystring/*.js 4.51 KiB 3 modules
modules by path ./node_modules/mini-css-extract-plugin/dist/hmr/*.js 5.14 KiB
  ./node_modules/mini-css-extract-plugin/dist/hmr/hotModuleReplacement.js 4.35 KiB [built] [code generated]
  ./node_modules/mini-css-extract-plugin/dist/hmr/normalize-url.js 811 bytes [built] [code generated]
4 modules
webpack 5.57.1 compiled successfully in 1880 ms
ℹ ｢wdm｣: Compiled successfully.
```

... значит, у пользователя на машине стояла версия 16 Node.js, когда он разрабатывал свой проект; возможная ошибка кроется в логах и конткретно в этом файле - _webpack/lib/DefinePlugin.js_.