---
layout: post
title: Github page customize
---

# Github page customize
Github page를 만들고 맘에 들었다가 이내 디자인이 맘에 걸려온다.  
이 부분을 어찌하였든 수정을 해야 하겠는데.. 어쩌나 싶다.  
아직 해야 할 것들이 있어서... 틈틈히 수정해야 겠다.

## Adding Comments Plugin
    comments를 작성할 수 있게끔 하고 싶어서 인터넷에 찾아보니 사용할 수 있는 몇개 안되는 plugins들을 찾을 수 있었다.  
    그런데 이리저리 보니 맘에 들지 않아서 [Facebook Comments Plugin](https://developers.facebook.com/docs/plugins/comments?locale=ko_KR) 을 적용하였다. 

### facebook app을 만든다. 

[facebook for developers](https://developers.facebook.com/apps/) 에서 app을 만든다. 

### app 설정

1. [app list](https://developers.facebook.com/apps/)에서 만들어진 app을 선택.
2. setting 메뉴로 들어간다.
3. `Contact Email`을 입력하고 `저장`한다. 
4. `App Review`메뉴로 들어간다.
5. `Make {app name} public`을 통해 생성한 app을 공개시킨다.

### Github page 적용

#### Facebook 작업

1. [Comments Plugin](https://developers.facebook.com/docs/plugins/comments?locale=ko_KR) 에서 
2. **Comments Plugin Code Generator** 섹션에 있는 `Get code`를 클릭.  
    ![Get Code](/img/plugin_Get_code.png)
3. *앱ID*에서 생성한 app을 선택한다. 
4. 첫 번째 코드 블럭을 카피한다.
 
~~~javascript
        <div id="fb-root"></div>
<script>(function(d, s, id) {
  var js, fjs = d.getElementsByTagName(s)[0];
  if (d.getElementById(id)) return;
  js = d.createElement(s); js.id = id;
  js.src = "//connect.facebook.net/ko_KR/sdk.js#xfbml=1&version=v2.5&appId=224630587608504";
  fjs.parentNode.insertBefore(js, fjs);
}(document, 'script', 'facebook-jssdk'));</script>
        ~~~
#### Github page 작업  

 작성한 post에서만 plugin를 연동할 생각이고, 난 아직 Jekyll 를 잘 알지 못한다.  
 Jekyll의 대충 구조를 참고하고, [Facebook Comments and Jekyll](https://joshuacox.github.io/jekyll/2015/11/28/facebook-comments-and-jekyll/)과 [Using-facebook comments with Jekyll](https://projectchilli.com/blog/2012/02/01/using-facebook-comments-with-jekyll/) 을 참고 하였다. 

1. `_layouts/default.html` 파일에서 `<body>` 안에 카피한 코드 블럭을 추가.
2. `_includes/head.html` 파일에 `<meta property="fb:app_id" content="{앱ID}" />` 를 추가. ({앱ID}는 카피한 코드 블럭의 `js.src = "//connect.facebook.net/ko_KR/sdk.js#xfbml=1&version=v2.5&appId=224630587608504"` 를 참고. )
3. `_layouts/post.html`의 `</article>`바로 위에 아래의 코드를 추가.
        ~~~html
        <hr/>
    <h3>Comments</h3>
    <div class="fb-comments" data-href="{{ site.url }}{{ page.url }}" data-num-posts="5"></div> 
</article>
        ~~~

## 참고 페이지

1. [Boxer's Frontend](http://boxersb.github.io/etc/2013/04/03/jekyll-introduction/)


