---
layout: post
title: Timeline.js
tags: [timelinejs, jekyll]
category: [Front-end]
---

> 그래도 첫 페이지인데, 신경을 넘 안쓴것 같아 [TimelineJS](https://github.com/NUKnightLab/TimelineJS3)를 붙여보았다. 
> 일단, 보기엔 좋넹.

![TimelineJS](/img/applying-timelinejs.png)



# 필요 재료

1. [TimelineJS](https://github.com/NUKnightLab/TimelineJS3) 에서 라이브러리를 다운로드 및 압축을 풀고
2. `compiled` 디렉토리에 있는 `css\`, `js\` 디렉토리를 copy.

# jekyll 수정

1. `_includes`의 `default.html`
    1. `index` page일 경우에만 timeline이 보여지도록 하기위해서, `page.path == 'index.md'`로 판단하여 필요한 `css`, `js`를 include
2. timelineJS의 data
    1. `site.posts` 를 이용하여 timelineJS의 data json 형태로 추출.
    2. image를 추출하기 위해 [In Jekyll How do i grap a post's first image?](http://stackoverflow.com/questions/25463865/in-jekyll-how-do-i-grab-a-posts-first-image)를 참고.  

~~~jekyll
{% raw %}
{% for post in site.posts %}    
        {
         'start_date':new Date('{{ post.date | date_to_xmlschema }}'),     
         'text':{
            'headline':'{{ post.title }}',
            'text': '<a href="{{post.url}}">{{ post.title }}</a>'
          }
          {% assign foundImage = 0 %}
            {% assign images = post.content | split:"<img " %}     
            {% for image in images %}
                {% if image contains 'src' %}
                    {% if foundImage == 0 %}
                        {% assign html = image | split:" " | first %}
                        {% assign img = html | split:"\"" | last %}
                        {% assign src = img | split:"\"" | first %}
                        {% assign src = src | split:"=" | last %}        ,
        'media':{
            'caption':'',
            'url':{{src}}
        },
                    {% assign foundImage = 1 %}
                    {% endif %}
                {% endif %}
            {% endfor %}
        },
        {% endfor %}
{% endraw %}

~~~
    



