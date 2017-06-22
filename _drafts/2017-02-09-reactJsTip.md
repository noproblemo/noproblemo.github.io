---
layout: post
title: reactjs
---

## import syntax 
> [How to import and export components using React+ES6+webpack?](http://stackoverflow.com/questions/33956201/how-to-import-and-export-components-using-react-es6-webpack)  

To export a single component in ES6, you can use export default as follows:  
~~~javascript
class MyClass extends Component {
 ...
}

export default MyClass;
~~~

And now you use the following syntax to import that module:

~~~javascript
import MyClass from './MyClass.react'
~~~

If you are looking to export multiple components from a single file the declaration would look something like this:  

~~~javascript
export class MyClass1 extends Component {
 ...
}

export class MyClass2 extends Component {
 ...
}
~~~

And now you can use the following syntax to import those files:  
~~~javascript
import {MyClass1, MyClass2} from './MyClass.react'
~~~

## sublime text setting
> [Sublime3玩转ES6+ReactJs](http://www.jianshu.com/p/84d50bc488da)


## Composition vs Inheritance

React has a powerful composition model, and we recommend using composition instead of inheritance to reuse code between components.  
Anything inside the <FancyBorder> JSX tag gets passed into the FancyBorder component as a children prop. Since FancyBorder renders {props.children} inside a <div>, the passed elements appear in the final output.

 ~~~javascript
 function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}
    </div>
  );
}
~~~

~~~javascript
function WelcomeDialog() {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        Welcome
      </h1>
      <p className="Dialog-message">
        Thank you for visiting our spacecraft!
      </p>
    </FancyBorder>
  );
}
~~~

## Refs and the DOM
> 전형적인 React dataflow에서 props들은 parent components들과 그들의 children들 사이의 interact를 할 수 있는 유일한 방법이다. child를 modify하게되면, new props를 가지고 re-render가 된다.  
> However, there are a few cases where you need to imperatively modify a child outside of the typical dataflow. The child to be modified could be an instance of a React component, or it could be a DOM element. For both of these cases, React provides an escape hatch.

### When to Use Refs   

refs를 사용을 위해 고려할만한 몇개의 좋은 예
 # text select 또는 media playback의 foucs를 managing 할 때
 # 필수 animations을 triggering 할 때
 # third-party DOM libraries를 통합하려 할 때

Avoid using refs for anything that can be done declaratively.

## [Handle events by arrow function in React app](https://medium.com/@machnicki/handle-events-in-react-with-arrow-functions-ede88184bbb#.yeketvbqe)
> constructor에서 handler를 bind 하지 않고 이벤트를 bind할 수 있다. 

~~~javascript
constructor(props){
  super(props);
  this.handleFilterTextInputChange = this.handleFilterTextInputChange.bind(this);  
}

handleFilterTextInputChange() {
  
}

render(){
    return (
      <form>
        <div><input type="text" placeholder="Search.." value={this.props.filterText} onChange={this.handleFilterTextInputChange} /></div>        
      </form>
    );
  }
~~~

~~~javascript
constructor(props){
  super(props);  
}

handleFilterTextInputChange() {
  
}

render(){
    return (
      <form>
        <div><input type="text" placeholder="Search.." value={this.props.filterText} onChange={(e)=>this.handleFilterTextInputChange(e)} /></div>        
      </form>
    );
  }
~~~


## Lists and Keys
> [List and Keys](https://facebook.github.io/react/docs/lists-and-keys.html) - In React, transforming arrays into lists of elements is nearly identical.  

You can build collections of elements and include them in JSX using curly braces `{}`.

~~~javascript
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li>{number}</li>
);
~~~
자바스크립트의 `map()`함수를 이용하여 `number` 배열을 looping 하여 각 아이템을 위한 `<li>`element를 리턴하고 마지막으로 `listItems`로 elements 배열의 결과를 assign한다. 
그리고, 전체 `listItems` 배열을 `ul` element 안에 include하고 render it to the DOM 한다.   
~~~javascript
ReactDOM.render(
  <ul>{listItems}</ul>,
  document.getElementById('root')
);
~~~

일반적으로 component안에 lists들을 render 할 것이다. 이전 예들을 numbers 배열을 받아서 elements의 unordered list로 출력하는 component로 refactor하면

~~~javascript
function NumberList(props){
  
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
   document.getElementById('root')
);
~~~

이 코드를 실행 시키면 list item은 key가 있어야 한다는 warning을 볼 것이다. "key"는 element 리스트를 생성할 때 필요한 special string attibute 이다. 
`numbers.mp()` 안의 list items에 key를 할당 시켜 missing key issue를 수정할 것이다.
~~~javascript
function NumberList(props){
  const numbers = props.numbers;
  const listItems = numbers.map((number)=>
    <li key={number.toString()}>
      {number}
    </li>
  );

  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers = {numbers} />,
  document.getElementById('root')
);
~~~


### Keys
> keys는 어떤 items이 변경되어졌는지, 추가되었는지, 삭제되어졌는지를 구별하는데 도움을 준다. Keys should be given to the elements inside the array to give the elements a stable identity:
~~~javascript
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);
~~~

key를 선택하는 가장 좋은 방법은 uniquely identifies a list item among its siblings. Most often you would use IDs from your data as keys:
~~~javascript
const todoItems = todos.map((todo) =>
  <li key={todo.id}>
    {todo.text}
  </li>
);
~~~

When you don't have stable IDs for rendered items, you may use the item index as a key as a last resort:
~~~javascript
const todoItems = todos.map((todo, index) =>
  // Only do this if items have no stable IDs
  <li key={index}>
    {todo.text}
  </li>
);
~~~