---
layout: post
title: Kotlin When
categories: kotlin_study
comments: true
tags: kotlin When
date: 2019-10-12
author: kawa1lg1rl
---

## When
switch문과 많이 비슷하다.

### 사용법

switch처럼 사용하는 방법
```kotlin
when(x) {
    1 -> println(1)
    2 -> println(2)
    3,4 -> println("over 2")
    in 5..10 -> println("5~10")
    else -> println("else")
}

```

switch와 if를 섞은것처럼 사용
```kotlin 
var a = 50
when() {
    a <= 10 -> println("a <= 10")
    else -> println("a > 10")
}
```