---
layout: post
title: Kotlin Constructor
categories: kotlin_study
comments: true
tags: kotlin constructor
date: 2019-10-12
author: kawa1lg1rl
---


## Constructor

코틀린의 생성자는 자바와는 조금 다른 방식으로 선언한다.

### 생성자 정의 방식
```kotlin
class Test {
    constructor() {
        ...
    }

    constructor(number: Int) {

    }
}
```

```kotlin
class Test constructor(var _number: Int) {
    var number = _number
}

class Test(var _number: Int) {
    var number = _number
}


class Test(var _number: Int = 1 ) {
    var number = _number
}
```
기본값을 설정할 수도 있다. 


### init

```kotlin
class Test(var _number: Int) {
    var number: Int = 0

    init {
        number = _number
        println("number = $number")
    }
}
```