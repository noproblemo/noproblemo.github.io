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


## install webpack Library
`react` 라이브러리들을 설치했으면, [Setting Up Webpack for React and Hot Module Relacement] 에서와 같이 `webpack`을 설치해 준다.  

~~~bash
$ npm install webpack --global
$ npm install webpack --save-dev
~~~

----
[Getting Started - React]: https://facebook.github.io/react/docs/getting-started.html  "Getting Started"  
[npm]: https://www.npmjs.com/  "node package manager"  
[grunt]: http://gruntjs.com/getting-started  "Getting started"  
[webpack - module bundler]: https://webpack.github.io  "webpack module bundler"  
[Setting Up Webpack for React and Hot Module Relacement]: https://robots.thoughtbot.com/setting-up-webpack-for-react-and-hot-module-replacement  "Setting Up Webpack for React and Hot Module Replacement"  
[webpackKor]: http://yourakmoon.blogspot.kr/2015/06/react-js-hot-module-replacement-webpack.html  "React js 와 Hot Module Replacement 를 위한 Webpack 세팅"  
[webpack 소개]: http://blog.hckrmn.net/2016/02/05/webpack-%EC%86%8C%EA%B0%9C/  "Webpack 소개"  
[reactWithWebpack]: http://jslog.com/2014/10/02/react-with-webpack-part-1/  "React with webpack"  
[egghead]: https://egghead.io/lessons/react-building-a-react-js-app-up-and-running-with-react-and-webpack "Build Your First React.js App"  
[Babelify]: http://easyreactbook.com/blog/react-fundamentals-configuring-browserify-babelify-and-react  "React Fundamentals: Configuring Browserify Babelify and React"  
[syntaxError]: http://stackoverflow.com/questions/33460420/babel-loader-jsx-syntaxerror-unexpected-token  "babel-loader jsx SyntaxError: Unexpected token"



