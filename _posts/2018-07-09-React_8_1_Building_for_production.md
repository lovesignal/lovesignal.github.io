---
key: 20180709
title: "[React] Movie app clone coding : Building for production"
excerpt: "movie app 만들기 - Building for production"
categories: programming
comments: true
tags: [clonecoding, react, javascript, jsx]
---



# 8-1. Building for production

## Github pages

static file을 올릴 수 있는 서비스.

static file은 자바스크립트, css, html과 같은 frontend 파일을 의미한다 (backend는 안됨).

Github page는 이러한 static file을 무료로 호스팅할 수 있게 해준다.

<br>

### 필요한 것 세가지

1. Github 계정
2. Github Project
3. Github Project의 branch : 이름은 gh-pages로 해야 한다.

<br>

<br>

## Build

1. `yarn build`  : CSS를 가져다가 압축한다. 로컬호스트에 있을 때 사용하는 코드는 압축되어 있지 않고, 느리고 최적화되어 있지 않다. `build` 작업을 하면 좀더 최적화 되고, 압축, 향상되는 것이다. 

<br>

2. `package.json` 으로 가서 `key` 를 추가한다. 

```javascript
{
  ...
  "homepage" : "http://lovesignal.github.io/movie_list"
}
```

<br>

3. 다시 `yarn build` 를 실행하면 아래와 같은 메시지가 출력된다.

```shell
yarn run v1.7.0
$ react-scripts build
Creating an optimized production build...
Compiled successfully.

File sizes after gzip:

  41.38 KB  build/static/js/main.5302de1f.js
  771 B     build/static/css/main.6c472154.css

The project was built assuming it is hosted at /movie_list/.
You can control this with the homepage field in your package.json.

The build folder is ready to be deployed.
To publish it at http://lovesignal.github.io/movie_list, run:

  yarn add --dev gh-pages

Add the following script in your package.json.

    // ...
    "scripts": {
      // ...
      "predeploy": "npm run build",
      "deploy": "gh-pages -d build"
    }

Then run:

  yarn run deploy

Find out more about deployment here:

  http://bit.ly/2vY88Kr

✨  Done in 5.02s.
```

<br>

4. `yarn add --dev gh-pages` 를 실행한다.

```shell
yarn add v1.7.0
[1/4] 🔍  Resolving packages...
⠂ gh-pages(node:1659) [DEP0005] DeprecationWarning: Buffer() is deprecated due to security and usability issues. Please use the Buffer.alloc(), Buffer.allocUnsafe(), or Buffer.from() methods instead.
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
[4/4] 📃  Building fresh packages...
success Saved lockfile.
success Saved 8 new dependencies.
info Direct dependencies
└─ gh-pages@1.2.0
info All dependencies
├─ filename-reserved-regex@1.0.0
├─ filenamify-url@1.0.0
├─ filenamify@1.2.1
├─ gh-pages@1.2.0
├─ humanize-url@1.0.1
├─ strip-outer@1.0.1
├─ strip-url-auth@1.0.1
└─ trim-repeated@1.0.0
✨  Done in 4.24s.
```

<br>

5. 그리고 아래 코드를  `packages.json` 의 `scripts` 에 추가한다.

```javascript
    "scripts": {
      // ...
      "predeploy": "npm run build",
      "deploy": "gh-pages -d build"
    }
```

<br>

6. 아래 명령어 실행

```shell
npm run build
yarn run deploy
```

<br>

적용되는데 5분 정도 걸린다.