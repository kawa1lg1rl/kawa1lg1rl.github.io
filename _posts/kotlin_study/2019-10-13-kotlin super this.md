---
layout: post
title: Kotlin Super This
categories: kotlin_study
comments: true
tags: kotlin 
date: 2019-10-13
author: kawa1lg1rl
---


## super

```kotlin
open class A() {
    fun a() { 
        println(1)
    }
}
class B: A() {
    override fun a() {
        println(2)
    }

    inner class C() {
        var b = B()
        b.a() // 2
        super@b.a() // 1 
    }
}
```


```kotlin
// A : class
// B : interface

class C: A(), B{ 
    override fun test() {
        // A와 B에 둘다 test 메서드가 있을 때
        super<A>.test()
        super<B>.test()
    }
}

```