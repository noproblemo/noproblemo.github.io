---
layout: post
tags: [React, React Native]
category: [React Native, Front-end, iOS]
---

# REACT BASIC

## component의 기본 구조
>화면에만 집중한다. 

```js
var Example = React.createClass({
	render:function(){
	}
})
```

## component들의 구조
> TopDown 구조를 가진다.  
> 하나의 parent element를 가져야만 한다. 

```js
var Example = React.createClass({
	render:function(){
		return (
			<View>
				<Text>line 1</Text>
				<Text>line 1</Text>
			</View>
		)		
	}
})
```

## state와 property의 적절한 사용

### Property
> Parent Component에서 child Component로 데이터를 넘겨줄 때 Property를 사용하여 넘겨 준다.  
> Property는 위에서 아래로 흐른다.(Top-Down)  
> 특별하게 Parent의 함수를 child에서 호출하게 하기위해 Property에 Parent 함수를 넘겨 줄 수 있다. 

```js
var Example = React.createClass({
	render:function(){
		return (
			<View>
				<Text name={'test1'}>line 1</Text>
				<Text name={'test2'}>line 1</Text>
			</View>
		)		
	}
})
```

```js
var Example = React.createClass({
	_callParent:function(){
		console.log('call parent function from child');
	},
	render:function(){
		return (
			<View>
				<Text name={'test1'} parentFunc={this._callParent} >line 1</Text>
				<Text name={'test2'}>line 1</Text>
			</View>
		)		
	}
})
```


### State
> state의 초기 값은 ```getInitialState``` 함수에서 설정 할 수 있다 .  
> ```getInitialState```함수와 같은 component method들은 특별한 [lifecycle](https://facebook.github.io/react/docs/component-specs.html) 를 따른다.  
> state의 변경의 따라 render(화면 갱신)가 된다.  
> 따라서 render 하기위해 state값을 변경시키므로(**setState({})**) render 함수 안에서 state를 set할 수 없다.  
> 이에 state값을 어디서 변경해야 하는 것이 문제가 됨.  
> 왜냐하면 state 값을 변경하면 이와 관련되어 있는 모든 component들의 view가 업데이트가 되고, 이 state값을 변경하기 위해 넘어온 값들을 state에 적용해 주어야 하는데, 넘어온 값을 받을 수 있는 곳은 render 함수를 통해서 할 수 있기 때문이다.  뿐만아니라 state값이 parent에도 있을 수 있고, child에서 있을 수 도 있다.  
> 물론, component method 들을 이용하여 어느정도 할 수 는 있겠지만 절대적으로 다 해결되지 않는다.  
> 그래서 이때부터 코드가 코이기 시작하고 복잡해지기 시작한다.  flex및 redux 가 자주 보이는 이유는 이 때문이다.  
> flux, redux는 pub, sub의 이벤트 구조에 state를 가지는 데이터 구조로 보면 된다. 

```js
var Example = React.createClass({
	getInitialState:function(){
		return ({
			parentValue:[]
		});
	},
	_callParent:function(){
		console.log('call parent function from child');
	},
	render:function(){
		return (
			<View>
				<Text name={'test1'} parentFunc={this._callParent} >line 1</Text>
				<Text name={'test2'} parentValue={this.state.parentValue} >line 2</Text>
			</View>
		)		
	}
})
```

# REACT NATIVE PRACTICAL
* https://codepen.io/asommer70/post/react-native-habit-navigation

## LAYOUT

**flex** 를 이용해서 layout 및 css를 이용해서 색상을 잡는다. 

### Flexibile boxes concept
> flex layout의 모양을 정의한다는 것은 어떠한 display device의 가능한 공간에 가장 적합하게 채울 수 있게 width와 height를 수정할 수 있는 능력이 있다는 것이다. flex container는 가능한 여유 공간에 items들을 확장하여 채우거나 또는 넘치는 것을 막기위해 줄어들게 할 수 있다. 
> 

![Flexible boxes vocabulary](https://developer.mozilla.org/files/3739/flex_terms.png)

### Flex container
 flex container는 flex를 사용하거나 display property의 inline-flex값을 사용하여 정의되어진다. 
 
### Flex item
 flex container의 각 child들은 flex item이 된다. Text directly contained in a flex container is wrapped in an anonymous flex item. (text는 익명 flex item에 쌓여서 flex container에 포함되어 진다.)
 
### Axes 
 모든 flexible box layout은 두개의 축(axes)을 따른다. The main axis is the axis along which the flex items follow each other. The cross axis is the axis perpendicular to the main axis.
 
 * flex-direction property는 main axis 기반한다. 
 * justify-content property는 현재 라인의 main axis를 따라 flex item들이 어떻게 laid out할 지를 정의한다. 
 * align-items property는 현재 라인의 flex items들을 cross axis 따라 어떻게 laid out 할지를 정의 한다. 
 * align-self property는 single flex item을 어떻게 cross axis에 sligned할지와 align-items에 의해 established할 지를 정의한다. 

### 읽어볼 것들
* [A guide to flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
* https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes
* http://blog.krawaller.se/posts/a-react-app-demonstrating-css3-flexbox/

## Animation
lib를 사용하면 animation이 되긴 하지만, 필요한 작동을 적용시키는게 어렵당.  
css animation을 해야 하는건가? 아닌건가 혼란 스럽당. 



## Flux, Redux

Flux applications는 3개의 주요한 **dispatcher**, **stores**, **views** 파트로 구성되어 있다. _Model-view-controller와 혼동하지 말라._  
React view에서 사용자의 interacts가 발생할 때 view는 central dispatcher를 통헤 action을 application의 data 또는 business logic을 가지고 있는 다양한 stores에 전파하여 관련되어진 모든 view를 update한다.  
이러한 동작은 React의 programming style과 잘 맞아서 which allows the store to send updates without specifying how to transition views between states.  
모든 데이터는 centeral hub와 같은 **dispatcher**를 통해 흐르고, **Action**은 대부분 **views**와 user interaction으로 부터 비롯되며 **action creators**는 **dispatcher**를 호출 하는 것 밖에 없다. **dispatcher**은 **store**에 registred되어진 callbacks들을 invokes하고 effectively dispatching the data payload contained in the actions to all stores.

### Redux

* [Redux](https://dobbit.github.io/redux/index.html)
* [Leveling Up with React: Redux](https://css-tricks.com/learning-react-redux/)
 * [Guide 3: Redux](https://github.com/bradwestfall/CSS-Tricks-React-Series/tree/master/guide-3-redux)  
* [Counter Example : example react native redux](https://github.com/alinz/example-react-native-redux/tree/master/Counter)

## STORE
> Redux는 하나의 **store**에 모든 상태를 객체 트리 구조로 저장함.   

```js
{
	visibilityFilter:'SHOW_ALL',
	todos:[{
		text:'Consider using Redux',
		completed: true
	}, {
		text:'Keep all state in a single tree',
		completed: false
	}]
```

## ACTION
>
> 저장되어 있는 상태를 변화시키는 유일한 방법은 **액션 객체**를 전달하는 방법 뿐이다.  
> **액션은** 애플리케이션에서 store로 보내는 데이터 묶음.  
> 이 **액션은** ```store.dispatch()```를 통해 보낼 수 있다.  
> 
> 액션은 반드시 어떤 형태의 액션이 실행될지 나타내는 문자영형의 ```type``` 필드를 가져야 함.  
> ```type```외에 액션 객체의 구조는 마음대로.

```js
store.dispatch({
	type:'COMPLETE_TODO',
	index:1
});

store.dispatch({
	type:'SET_VISIBLITY_FILTER',
	filter:'SHOW_COMPLETED'
});
```
### 액션 생산자
> action을 만드는 함수 

```js
function addTodo(text) {
	return {
		type:ADD_TODO,
		text
	}
	
}
```

> 액션을 보내려면 결과값을 ```dispatch()``` 함수에 넘기면 됨.  
 
```js
dispatch(addTodo(text));
dispatch(completeTodo(index));
```

> 아니면 자동으로 액션을 보내주는 **바인드된 액션 생산자**를 만든다.   

```js
const boundAddTodo = (text)=>dispatch(addTodo(text));
const boundCompleteTodo = (index)=>dispatch(completeTodo(index));
```

> ```dispatch()``` 함수를 스토어에서 ```store.dispatch()```로 바로 접근할 수 있지만, react-redux의 ```connect()```와 같은 헬퍼를 통해 접근할 것임.   
> 여러 액션 생사자를 ```dispatch()```에 바인드하기 위해 ```bindActionCreateors()```를 사용할 수 도 있다. 


### sample code

```js
/* 
 * 액션 타입
 * /
export const ADD_TODO = 'ADD_TODO';
export const COMPLETE_TODO = 'COMPLETE_TODO';
export const SET_VISIBILITY_FILTER = 'SET_VISIBILITY_FILTER';

/*
 * 다른 상수
 * /
export const VisibilityFilters = {
	SHOW_ALL : 'SHOW_ALL',
	SHOW_COMPLETED: 'SHOW_COMPLETED',
	SHOW_ACTIVE: 'SHOW_ACTIVE'
};

/*
 * 액션 생산자 
 * /
export function addTodo(text) {
	return { type:ADD_TODO, text };
}

export function completeTodo(index) {
	return { type:COMPLETE_TODO, index };
}

export function setVisibilityFiler(filter) {
	return { type:SET_VISIBILITY_FILTER, filter };
}

```

## Reducer

> 액션에 의해 상태 트리가 어떻게 변화하는지를 지정하기 위해 **순수 리듀서**를 작성해야 함.  
> 리듀서는 그저 _이전 상태와 액션을_ 받아 _다음 상태를 반환하는_ 순수 함수. 이전 상태를 변경하는 대신 새로운 상태 객체를 생성해서 반환해야 함. 

```js
function visibilityFilter(state='SHOW_ALL', action) {
switch(action.type) {
	case 'SET_VISIBILITY_FILTER':
		return action.filter;
	default:
		return state;
	}
}

function todos(state=[], action) {
	switch (action.type) {
		case 'ADD_TODO':
			return [...state, {
				text:action.text,
				completed:false
			}];
		case 'COMPLETE_TODO':
			return [
				...state.slice(0, action.index), 
				Object.assign({}, state[action.index], {
					completed:true
				}),
				...state.slice(action.index+1)
				];
		default:
			return state;
	}
}

import { combineReducers, createStore }	from 'redux';
let reducer = combindeReducers({visibilityFilter, todos});
let store = cerateStore(reducer);				
```


 
### Flux

* [Flux TodoMVC Example](https://github.com/facebook/flux/tree/master/examples/flux-todomvc)
 * [Tutorail - Todo List](http://facebook.github.io/flux/docs/todo-list.html)


****