---
layout: post
title: jekyll view post list
categories: github_blog
comments: true
tags: jekyll
date: 2019-10-11
author: kawa1lg1rl
---

## 하단 글목록 생성
하단에 최근 포스팅 10개를 보여주는 박스를 넣어놨다.  

```html
<div class="more-posts" style="width:90%; max-width:1000px; margin: 0 auto;">
        <div class="more-category">
          <h4>Recent Posts</h4>
        </div>
        <table style="margin: 0 0 0 0">
          <tbody>
            {% assign count = 0 %}
            {% assign work_items = site.posts | sort: 'date' | reverse %}
            {% for post in work_items %}
              {% if post.categories != "test" %}
                {% assign count = count | plus: 1 %}
                {% if count < 11 %}
                  <tr>
                    <td class="more-posts-date">{{ post.date | date: '%Y. %m. %d' }}</td>
                    <th class="more-posts-title" style="border-bottom: 0px">
                      <a href="{{ site.url }}{{ post.url }}" style="shadow: 0 0 0; text-decoration: none"> [ {{ post.categories }} ] {{ post.title }}</a>
                    </th>
                  </tr>
                {% endif %}
              {% endif %}
            {% endfor %}
          </tbody>
        </table>
      </div>
```
