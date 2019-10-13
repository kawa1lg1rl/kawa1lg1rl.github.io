---
layout: post
title: Kotlin 상속과 다형성
categories: kotlin_study
comments: true
tags: kotlin Inheritances Polymophism Overload Override
date: 2019-10-13
author: kawa1lg1rl
---
## 상속

### Any
코틀린에서는 기본적으로 상속클래스를 지정하지 않았을 경우 `Any`클래스를 묵시적으로 상속받는다.

### open
클래스 선언 시 `open` 키워드를 앞에 붙이게 되면 상속가능한 클래스가 된다.

```kotlin

open class Parent() {

}

class Child : Parent() {

}
```
## 다형성
같은 이름이지만 다른 행동을 취할 수 있게 하는 것

오버로딩과 오버라이딩이 있다.

### 오버로딩

```kotlin
fun test(a:Int) {

}

fun test(b:String) {

}
```

위 코드의 test함수는 이름은 서로 같지만 들어오는 인자의 type에 따라 다른 함수가 실행된다.

### 오버라이딩

코틀린에서는 부모 클래스의 오버라이딩할 메서드에도 open을 붙여줘야한다.  
또한 자식클래스에서 오버라이딩을 후, 자신을 상속받을 클래스에서의 오버라이딩을 막고 싶다면 final을 사용하면 된다.

```kotlin
open class Parent {
    open fun test() {
        println("parent test called")
    }
}

// 오버라이딩
class Child1 : Parent(){
    override fun test() {
        super.test()
        println("Child test called")
    }
}

// Child2를 상속한 클래스에서 test메서드 오버라이딩 방지
class Child2 : Parent() {
    final override fun test() {
        super.test()
    }
}
```

