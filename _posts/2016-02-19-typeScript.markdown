---
layout: post
title: typeScript
---
{% include JB/setup %}

# typeScript

요새 react native를 보고 있는데, 여러 문제가 발생했다. 
지금까지 듣도 보도 못했던, [arrow function](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/%EC%95%A0%EB%A1%9C%EC%9A%B0_%ED%8E%91%EC%85%98) 이라던가....  
그!런!데...
일단 아래와 같은 소스를 보면, 

~~~javascript
cloneWithRowsAndSections(
      dataBlob: any,
      sectionIdentities: ?Array<string>,
      rowIdentities: ?Array<Array<string>>
  ): ListViewDataSource {
    ...
  }
~~~

뭔가 알듯하면서도 아득하다.  

기본적으로 인수에 `:` 가 type을 지정한것은 알겠는데, `function():` 는 뭐더냐???  
구글링을 해보아도 안나오고... 슬슬 짜증이 나기 시작했다.  
이때부터 머리는 이미 생각의 한계를 그어놓고 있었다.  

일단, 별것도 아닌것 같으니 문맥만 이해하고 넘어가기로 하고 나머지 소스를, 예제를 보며 넘어가는데 계속 `function():` 이 눈에 거슬려 진도가 안나가기 시작한다.  

짜증이 폭팔할것 같았다. 문맥을 이해하는데있어, `:` 는 아무 상관이 없었지만 모든 소스에, 예제에 줄기차게 출현하는 저 신택스!!!! 마치 코를 파다 파기엔 너무 고통스럽게 깊숙히 있어 미쳐파질 못해 남아 있는 코딱지 마냥 자꾸 신경이 쓰이는 것처럼..  
미치게 만든다.  
만으로 2틀 만에 우연히 검색하다 알게 [typescript](http://www.typescriptlang.org/) 되었지만, 알고 보니 더 짜증이 난다.  

아.. 짜증나...



 * reference : [TypeScript를 이용하여 javascript를 객체지향 언어처럼 사용해보자](http://cyberx.tistory.com/60)
