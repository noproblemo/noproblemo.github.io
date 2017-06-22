---
layout: post
title: react.js Break Down From Sample
---

# React 재입문

> React를 처음 접한게 작년 여름 정도인것 같은데... 
> Divide and Conquer
> 개발 환경 설정은 제외
> [Thinking in React](https://facebook.github.io/react/docs/thinking-in-react.html)

## Mock을 Html로 변환 
![Mock](https://facebook.github.io/react/img/blog/thinking-in-react-mock.png)

위의 화면을 html로 작성하면 
~~~html
<div>
	<form action="">
		<div><input type="text" placeholder="Search.."></div>
		<input type="checkbox"><span>Only show products in stock</span>
	</form>
	<div class="list">
		<table>
			<thead>
				<tr>
					<td>Name</td>
					<td>Price</td>
				</tr>
			</thead>
			<tbody>
				<tr>
					<td colspan="2"></td>
				</tr>
				<tr>
					<td>category</td>
					<td>product</td>
				</tr>
			</tbody>
		</table>
	</div>
</div>
~~~

리스트 데이터는 
~~~json
[
  {category: "Sporting Goods", price: "$49.99", stocked: true, name: "Football"},
  {category: "Sporting Goods", price: "$9.99", stocked: true, name: "Baseball"},
  {category: "Sporting Goods", price: "$29.99", stocked: false, name: "Basketball"},
  {category: "Electronics", price: "$99.99", stocked: true, name: "iPod Touch"},
  {category: "Electronics", price: "$399.99", stocked: false, name: "iPhone 5"},
  {category: "Electronics", price: "$199.99", stocked: true, name: "Nexus 7"}
];
~~~

## Break The UI into A Component hierarchy
> Divide and Conquer 를 적용해서 생각한다.  
> 유저 인터렉션하는 searching text를 입력하는 input box 하나, 아이템 상태를 filtering하는 checkbox 하나
> 리스트를 뿌려주는 부분은 카테고리를 출력하는 부분 하나, 해당 카테고리에 해당하는 아이템을 출력하는 부분 하나 로 구성되어 있다고 볼 수 있다. 
> 유저 인터렉션 하는 부분을 search bar로 naming 하고, 리스트를 뿌려주는 부분을 products table 이라고 naming 하자. 






