---
layout: post
title: Jekyll에 Bootstrap 적용
tags: [jekyll-bootstrap, facebook comments plugin]
---
{% include JB/setup %}

# Bootstrap 적용

> (GitHub Page에 Jekyll Bootstrap 적용하기)[http://sapzildj.github.io/etc/2015/08/10/Jekyll_Bootstrap/]를 참고함

## Install Jekyll-Bootstrap

* [jekyll-quick-start] (http://jekyllbootstrap.com/usage/jekyll-quick-start.html) 의 instruction을 참고하여 `git clone` 으로 새로운 이름을 적용하여 내려 받음 
* 기존의 `jekyll` 디렉토리에 카피하는데 중요한 파일들을 알아내기 위해 디렉토리 비교를 하였음.
* 혹시나 하는 마음에 기존 `jekyll` 디렉토리를 백업본으로 생성함
* 새로 내려받은 `jekyll-bootstrap`의 내용을 죄다 카피.
* 백업본으로 떠논 디렉토리에서 기존 `_post` 디렉토리, `_drafts` 디렉토리 안에 있는 파일들을 다시 카피.
* `_config.yml`을 알맞게 수정 
* `_includes/themes/bootstrap-3`에 있는 `defalut.html`, `post.html` 파일에서 기존의 facebook comments plugin을 추가했던 코드들을 복사하여 각각 수정.


