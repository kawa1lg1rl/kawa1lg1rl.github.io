---
layout: post
title: Kotlin Destructuring
categories: kotlin_study
comments: true
tags: kotlin destructuring
date: 2019-10-14
author: kawa1lg1rl
---

## Destructuring
예제를 보고 Python의 tuple이 떠올랐다.  
data class에서 사용할 수 있다.

### 소괄호로 Destructuring

소괄호를 이용해 data class를 분해할 수 있다.
```kotlin
fun main(args: Array<String>) {
    var user = Test("kawa1lg1rl", 21)

    var (name, age) = user

    println("user name : $name, user age : $age")
}


data class Test(var name: String, var age:Int) {

}
```

#### for문 응용
for문을 이용해 응용할 수도 있다.

```kotlin
fun main(args: Array<String>) {
    var users: Array<Test> = arrayOf()

    for(i in 0..10) {
        users = users.plus(Test("kawa1lg1rl", i))
    }

    for((name, age) in users) {
        println("user name : $name, user age : $age")
    }
}


data class Test(var name: String, var age:Int) {

}
```

#### 함수 응용
```kotlin
fun main(args: Array<String>) {
    var users: Array<Test> = arrayOf()

    for(i in 0..10) {
        users = users.plus(Test("kawa1lg1rl", i))
    }

    var (name, age)= users.getUserInfo(7)!!

    println("$name $age")
}

fun Array<Test>.getUserInfo(_age: Int) : Test? {
    for((name, age) in this) {
        if(age == _age) return Test(name, age)
    }
    return null
}


data class Test(var name: String, var age:Int) {

}
```


#### 람다식에서 사용
```kotlin
fun main(args: Array<String>) {
    var users: Array<Test> = arrayOf()

    for(i in 0..10) {
        users = users.plus(Test("kawa1lg1rl", i))
    }

    {(name, age):Test -> println("$name ,$age")}(users[10])

}

data class Test(var name: String, var age:Int) {

}
```

#### underscore
필요없는 프로퍼티는 _을 이용해 생략할 수 있다.

```kotlin
fun main(args: Array<String>) {
    var user = Test("kawa1lg1rl", 21)

    var (_, age) = user

    println("user age : $age")
}


data class Test(var name: String, var age:Int) {

}
```


### componentN method
data class의 componentN 메서드를 통해 분해할 수 있다.

```kotlin
fun main(args: Array<String>) {
    var user = Test("kawa1lg1rl", 21)

    var name = user.component1()
    var age = user.component2()

    println("user name : $name, user age : $age")
}


data class Test(var name: String, var age:Int) {

}
```
