---
layout: post
title: github jekyll blog with google analytics and disqus
categories: github_blog
comments: true
tags: google_analytics github jekyll disqus
date: 2019-10-11
author: kawa1lg1rl
---
## Github Jekyll Blog 개설

markdown 과 ruby를 이용하여 블로그를 운영할 수 있는 Jekyll이라는 템플릿이 있다.  
정적으로 운영이 가능하다.

Jekyll은 Github에서 지원해준다. 따라서 Github에 Jekyll을 검색하면  
나는 jekyll-theme-hacker를 사용하기로 했다.

### 테마를 적용한 개설 방법
1. github repository를 `nickname.github.io`와 같은 형식으로 생성한다.
2. `Settings`에 들어가 `Github Pages`를 설정한다. 
3. _config.yml을 생성한 후 아래와 같은 코드를 입력한다.
```yml
title: blog title
description: description
theme: jekyll-theme-hacker
```

이 정도만 해줘도 테마를 적용해서 블로그 개설을 할 수 있다. 
위와 같은 코드를 입력하고 커밋하게 되면 
`https://nickname.github.io`로 들어가 메인페이지를 확인할 수 있다.  

하지만 나는 커스터마이징을 하려고 찾아보다보니 jekyll-theme-hacker 저장소를 받아서 사용하는게 더 편할거같아서 받아서 사용하고 있다.

~~remote-theme을 통해 자동으로 다운받아준다고 한다. 안되는 테마도 있다고..~~


### Google Analytics
블로그 커스터마이징을 진행하면서 방문자수를 보고싶었다.  
그래서 Google Analytics를 찾게 되었는데 Google Analytics를 가입하고 새 앱을 만든 뒤,  
발급받게 되는 id를 `_config.yml`에 적용해주면 된다.

```yml
title: kawa1lg1rl's blog
description: Hi
google_analytics: UA-149453934-1
theme: jekyll-theme-hacker
```

### 댓글 기능
댓글 기능은 disqus를 사용하였는데,  
Google Analytics와 비슷하다.

disqus 가입 후 `I want to install disqus on my web`이라는 버튼을 통해 웹페이지를 입력 한다.  
그 후 disqus_url과 disqus_name을 _config.yml에 적어주면 된다.
```yml
title: kawa1lg1rl's blog
description: Hi
google_analytics: UA-149453934-1
theme: jekyll-theme-hacker
disqus_url: https://kawa1lg1rls-github-blog.disqus.com
disqus_name: kawa1lg1rls-github-blog
```
## .
Disqus와 Google Analytics 둘 다 javascript 코드를 제공해준다.  
해당 코드를 default.html과 같은 필요한 곳에 입력하기만 하면 연동이 끝난다.