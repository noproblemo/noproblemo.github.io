---
layout: post
title: ReactJs 개발환경
tags: [ReactJS, Development Environment]
category: [Front-end, ReactJS, Environment]
---

![React](https://facebook.github.io/react/img/logo.svg)

> 기존의 font-end 개발환경과 같이 react도 grunt등과 같은 툴을 사용하여 개발 환경을 구축한다면 편하지 않을까 하여 정리함. 

# react의 Getting Strated 부터 
여러 페이지를 서칭하여 작업하다 보니, [Getting Started - React] 에서 만나더라,  
일단 서칭하기전에 여기부터...  
물론 [webpack - module bundler], [grunt], [npm] 등과 같은 library 를 __알고있다면__ 접하고 사용하는데 **많은 도움이 된다**.([webpack - module bundler]에 대해 들어본 적이 없다면, [webpack 소개]가 도움이 될 것 같다.)  

# 시작  
일단 프로젝트를 생성해야 하므로, 적당한 디렉토리를 만들고 해당 디렉토리로 옮겨서 [Setting Up Webpack for React and Hot Module Relacement]에서와 같이 다음의 명령으로 초기화를 진행한다. 

~~~bash
npm init
~~~

> `npm init` 을 하는 것은 `package.json`을 생성하기 위함이고, 여기서 중요한 점은 [Setting Up Webpack for React and Hot Module Relacement]에서도 나와 있지만, `"prevate":true`를 `npm init` 으로 생성된 `package.json`에 추가 한다는 것.  

~~~javascript
{
  "name": "test",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "private": true
}
~~~

## install ReactJs Library
이제 필요한 `react` 라이브러리들을 설치해야 하므로, [Getting Started - React]의 **Using React from npm** 섹션에서와 같이, [webpack - module bundler] 을 사용할 예정이니 다음의 dependency 들을 설치해야 겠다. 

~~~bash
$ npm install --save react react-dom babel-preset-react
~~~

그리고, babel과(jsx) 관련된 라이브러리 설치
~~~shell
$ npm install --save-dev babel-core babel-loader babel-preset-es2015
~~~


## install webpack Library
`react` 라이브러리들을 설치했으면, [Setting Up Webpack for React and Hot Module Relacement] 에서와 같이 `webpack`을 설치해 준다.  

~~~bash
$ npm install webpack --global
$ npm install webpack --save-dev
~~~



## 동강 시청
이쯤에서 [Build Your First React.js App - egghead] 를 시청해보자.  
텍스트로 쭈욱 보는 것이 **빠르다** 라고 생각할테지만, 항상 이제껏 그렇듯 **텍스트로 보는것은 기억력이 짧다**.  
주요하게 보아할 것은, 

1. 이제껏 설정한 것과 같은 과정을 거칠 것이며
2. 짧은 예제들과 연동하는 부분을 집중해서 보면 되겠다. 길지 않다. 약 8분 밖에 안된다. 

## webpack dev server install
> likes php static server.

아래와 같이 설치함.

~~~shell
$npm install webpack-dev-server --global
$npm install webpack-dev-server --save-dev
~~~

## Hot module replacement
[HMR]에 보면 코드를 수정 저장하면 webpack이 component state를 유지한체 페이지 리로딩 없이 module을 replace해 준다고 한다.  

~~~shell
$npm install react-hot-loader --save-dev
~~~

## Directory Structure
디렉토리 구조는 

~~~
-app
    -js
        -main.js
-public
    -js
    -index.html

~~~

이고, 테스트 코드는 [Getting Started - React]에 있는 `main.js`와 `index.html`을 사용함.(`index.html`의 경우 상황에 맞게 수정하였음.)

~~~javascript 
// main.js
var React = require('react');
var ReactDOM = require('react-dom');

ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('example')
);
~~~

~~~html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Hello React!</title>
  </head>
  <body>
    <div id="example"></div>
    <script src="bundle.js"></script>    
  </body>
</html>
~~~

## webpack.config.js 및 테스트 
동강에서 처럼 `webpack.config.js`를 현재 scaffold 구조에 맞게 작성 및 babel(jsx) 관련하여 `loaders`를 설정 및 `webpack -w` 로 결과 체크.

>만약 `new Error(Cannot define 'query' and multiple loaders in loaders list)`와 같은 에러가 발생하면, `loaders` 설정부분의 철자들을 체크.

`react-hot-loader`을 사용하기 위해 `loader` 객체를 수정해 준다. 

~~~javascript
module.exports = {
    context: __dirname + "/app",
    entry: "./js/main.js",
    output: {
        path: "./public/js",
        filename: "bundle.js"
    },
    module: {
        loaders: [{
            test: /\.jsx?$/,
            exclude: /node_modules/,
            loaders: ["react-hot", "babel-loader"],
            querys: {
                presets: ["react", "es2015"]
            }
        }, {
            test: /\.html%/,
            loader: "file?name=[name].[ext]"
        }]
    }
}
~~~

`webpack-dev-server --hot --inline content-base public/`으로 테스트.  

## 오작동
`webpack-dev-server --hot --inline content-base public/`으로 테스트를 해보면 **error**가 발생할 수 있다.(webpack-dev-server의 옵션은 [webpackDocs] 를 참고)  
이 경우엔 `.babelrc`를 아래의 내용으로 생성하면 된다.  

~~~javascript
{
        "presets":["es2015", "react"]
}
~~~



## 참고할 만한 문서들

1. [reactWithWebpack]
1. [webpackDocs]
1. [webpack Docs configuration]
1. [Developing with Webpack]
1. [Using Webpack Hot Module Replacement with React]
 

----
[Getting Started - React]: https://facebook.github.io/react/docs/getting-started.html  "Getting Started"  
[npm]: https://www.npmjs.com/  "node package manager"  
[grunt]: http://gruntjs.com/getting-started  "Getting started"  
[webpack - module bundler]: https://webpack.github.io  "webpack module bundler"  
[Setting Up Webpack for React and Hot Module Relacement]: https://robots.thoughtbot.com/setting-up-webpack-for-react-and-hot-module-replacement  "Setting Up Webpack for React and Hot Module Replacement"  
[webpackKor]: http://yourakmoon.blogspot.kr/2015/06/react-js-hot-module-replacement-webpack.html  "React js 와 Hot Module Replacement 를 위한 Webpack 세팅"  
[HMR]: http://webpack.github.io/docs/hot-module-replacement-with-webpack.html   "HOT MODULE REPLACEMENT WITH WEBPACK"    
[webpack 소개]: http://blog.hckrmn.net/2016/02/05/webpack-%EC%86%8C%EA%B0%9C/  "Webpack 소개"  
[reactWithWebpack]: http://jslog.com/2014/10/02/react-with-webpack-part-1/  "React with webpack"  
[Build Your First React.js App - egghead]: https://egghead.io/lessons/react-building-a-react-js-app-up-and-running-with-react-and-webpack "Build Your First React.js App"  
[Babelify]: http://easyreactbook.com/blog/react-fundamentals-configuring-browserify-babelify-and-react  "React Fundamentals: Configuring Browserify Babelify and React"  
[syntaxError]: http://stackoverflow.com/questions/33460420/babel-loader-jsx-syntaxerror-unexpected-token  "babel-loader jsx SyntaxError: Unexpected token"  
[webpackDocs]: https://github.com/webpack/docs/wiki/webpack-dev-server "webpack/docs"  
[webpack Docs configuration]:https://github.com/webpack/docs/wiki/configuration "configuration"   
[Developing with Webpack]: http://survivejs.com/webpack_react/developing_with_webpack/ "Developing with webpack"  
[Using Webpack Hot Module Replacement with React]:http://matthewlehner.net/react-hot-module-replacement-with-webpack/ "Using Webpack Hot Module Replacement with React"  
[code with github]: https://github.com/noproblemo/reactInit    "code with github"





