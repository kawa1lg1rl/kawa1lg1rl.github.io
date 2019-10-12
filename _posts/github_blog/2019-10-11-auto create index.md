---
layout: post
title: jekyll blog auto create index at post
categories: github_blog
comments: true
tags: 
date: 2019-10-11
author: kawa1lg1rl
---

## 목차 자동 생성
글을 잘 쓰지 못하다보니 목차를 생성하는게 글을 읽는데에 목차가 있으면 좋겠다는 생각이 들었다.  
그래서 javascript를 다시 쓰게 되었다..

heading 태그를 javascript로 파싱 후, ul li 태그를 통해 목차를 만들어줬다.
```javascript
<script>
     
  (function(){
    var main_contents = document.getElementById("main_content")
    var allHeadings = main_contents.querySelectorAll("h1, h2, h3, h4, h5, h6")
    var nicknameView = document.getElementsByClassName("view")[0]

    // 메인컨텐츠에 헤딩이 1개이상일때(제목빼고 더 있을때)
    if( allHeadings.length > 1 ) {
      // 목차 추가
      var temp_main = document.createElement("div")
      nicknameView.after(temp_main)
      temp_main.className = "custom_index"
      
      var beforeName = "null"
      var nodes = new Array()
      var beforeNumber = 0

      // i는 제목 pass용
      var isTitle = true
      var isFirstTag = true

      var nodesDepth = 0
      var count = 0
      for(var heading of allHeadings) {
        // 제목 pass 
        if(isTitle) { 
          isTitle = false 
          continue
        }
        
        var localName = heading.localName
        var localNumber = parseInt(localName[1])
        // 이전 태그와 이름이 다를경우 ul을 추가하거나,
        // 이전으로 돌아간다.
        // nodesDepth를 건드린다.
        if(localName != beforeName) {
          // 처음 시작일 경우 세팅
          if(isFirstTag) {
            isFirstTag = false
            var firstTag = document.createElement("ul")
            nodes.push ( firstTag )
            beforeNumber = localNumber
            nodesDepth = 0
          } else {
            // 헤딩태그 더 작은게 생겼을 경우, 
            // ul을 추가해야함.
            if(beforeNumber < localNumber) {
              var newUl = document.createElement("ul")
              nodes[nodesDepth].appendChild(newUl)
              nodes.push(newUl)
              nodesDepth += 1
            } else {
              nodesDepth -= 1
              nodes.pop()
            }

            beforeNumber = localNumber
          }
          beforeName = localName
        }
        
        var aTagBeforeHeading = document.createElement("a")
        var currentA = document.createElement("a")
        var currentLi = document.createElement("li")
        var currentH4 = document.createElement("h4")

        var name = "inPage_" + count
        aTagBeforeHeading.name = name            
        currentA.href = "#" + name
        currentA.style.textDecoration = "none"  

        currentH4.style.margin = "0px 0px 0px 0px"
        currentH4.style.color = "#e0e0e0"
        currentH4.style.fontWeight = "bold"

        currentH4.innerHTML = heading.innerHTML
        currentA.appendChild(currentH4)
        currentLi.appendChild(currentA)
        nodes[nodesDepth].appendChild(currentLi)

        heading.before(aTagBeforeHeading)

        count += 1
      }

      var indexString = document.createElement("h2")
      indexString.innerHTML = " - Index - "
      indexString.style.color = "#e0e0e0"
      indexString.style.fontWeight = "bold"

      temp_main.append(indexString)
      temp_main.append(nodes[0])
    }
  })()

</script>
```
