---
layout: post
title: Github page customize
tags: [jekyll-bootstrap, facebook comments plugin]
category: [blog, style, customize]
---
{% include JB/setup %}

Github page를 만들고 Github page에 [jekyll bootstrap][1] 적용한 후 스타일이 맘에 들지 않아 투덜대기만 하다, 일단 적용해 봄.

[Phabricator Phame][2]의 스타일이 왠지 좋아서, 일단 필요한 `css` 파일 및 `font` 관련된 리소스들을 죄다 카피 및 적용.  
jekyll의 파싱된`{content}`의 구조를 바꿔서 맞추려고 했지만, 능력의 부재로([liquid][3] 템플릿 엔진을 사용한다고 하는데... 뭔소린지 몰겠넹. 시간내서 파보는 것도 좋을 듯 함.) 인해 그냥 `custom` css를 하나더 생성하여 `{content}`의 결과에 맞추어 css를 수정 및 적용.

## 결과

Before   
![before](/img/before.png)






[1]: http://sapzildj.github.io/etc/2015/08/10/Jekyll_Bootstrap/ "Github page에 jekyll bootstrap 적용하기"
[2]: https://secure.phabricator.com/book/phabricator/article/phame/ "Phame User Guide"
[3]: https://github.com/Shopify/liquid/wiki "liquid"



