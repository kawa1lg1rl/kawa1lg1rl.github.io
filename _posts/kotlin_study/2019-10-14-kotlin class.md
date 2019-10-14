---
layout: post
title: Kotlin class
categories: kotlin_study
comments: true
tags: kotlin class
date: 2019-10-14
author: kawa1lg1rl
---

## Class
코틀린의 클래스와 관련된 것들을 적어놓은 문서

### Nested Class
* 자바의 static class처럼 사용할 수 있다. 
* 바깥쪽의 프로퍼티나 메서드에 접근할 수 없다.

```kotlin

class A {
    class B {

    }
}
```

B가 Nested class이다. 

```kotlin
class A {
    class B{

    }
}

fun test() {
    A.B()
}
```
A클래스의 객체 생성없이 B에 접근할 수 있다.


### Inner class
* 바깥쪽의 프로퍼티나 메서드에 접근할 수 있다.
    * private이더라도 접근 가능
* inner키워드를 작성해야한다.

```kotlin
class A {
    inner class B{ 

    }
}
```

B는 inner class이다.

```kotlin
class A {
    var testString = "test"
    inner class B{
        constructor() {
            println("A.testString : $testString")
        }
    }
}

fun test() {
    A().B()
}
```

B클래스 바깥의 프로퍼티인 `testString`에 접근할 수 있다.


### local class, anonymous class
* 지역 클래스는 지역변수처럼 해당 지역에서만 사용 가능한 클래스
* 익명 클래스는 object 키워드를 통해 생성 가능한 익명 클래스

#### 지역 클래스
```kotlin
fun test() {
    class A {
        constructor() {
            println("A")
        }
    }

    A()
}
```

#### 익명 클래스
```kotlin
fun test() {
    var anonClass = object {
        fun Hi(){
            println("Hello")
        }
    }

    anonClass.Hi()
}
```
익명 클래스는 아래처럼도 사용 가능하다.

```kotlin

interface Person {
    fun printUserInfo()
}


fun test() {
    var anonClass = object : Person{
        var name:String? = null
        var age:Int = 0

        override fun printUserInfo() {
            println("$name, $age")
        }
    }

    anonClass.name = "kawa1lg1rl"
    anonClass.age = 21


    anonClass.printUserInfo()
}

```



### Sealed class
봉인된 클래스(?)  
아직 어떻게 사용하는지 왜 사용하는지 잘 모르겠다.  


* sealed 키워드를 붙여서 사용한다.
* 기본적으로 상속 가능하다.
* 다른 파일에서 상속 불가능하다.
* 내부의 클래스도 open키워드를 붙여 상속가능하게 할 수 있다.

대충 아래와 같이 사용할 수 있다고 한다..

```kotlin
sealed class Creature {
    open class Person()
    open class Dog()
    open class Cat()
}

fun getName(creature: Creature): String =
        when (creature){
            is Creature.Person -> "Person"
            is Creature.Dog -> "dog"
            is Creature.Cat -> "cat"
            else -> "!?@#"
        }
```

```kotlin
sealed class Creature

open class Person : Creature()
open class Dog : Creature()
open class Cat : Creature()

fun getName(creature: Creature): String =
        when (creature){
            is Person -> "Person"
            is Dog -> "dog"
            is Cat -> "cat"
            else -> "!?@#"
        }
```
왜 이렇게 쓰는지, 언제 어떻게 쓰는지는 잘 모르겠다.


### Enum Class
혼자 개발할때 잘 안쓰던 Enum이라 알고 싶지 않았다.  
* enum 키워드를 붙인다.
* enum 안에 객체를 열거할 수 있다.
* 함수를 선언해서 각 객체에서 호출해 사용할 수 있다.  

```kotlin
fun main(args: Array<String>) {

    var test:Color = Color.GREEN

    println(test.name) // 이름
    println(test.ordinal) // 순서 
    println(test.toString()) // 이름
}

enum class Color(var r:Int, var g:Int, var b:Int) {
    RED(0xff, 0, 0), GREEN(0,0xff,0), BLUE(0, 0, 0xff)
}

```

또한 인터페이스를 구현할 수도 있다.

```kotlin

interface Test {
    fun printHello()
}

enum class Color(var r:Int, var g:Int, var b:Int) : Test{
    RED(0xff, 0, 0) {
        override fun printHello() {
            println("Hello")
        }
    }, GREEN(0,0xff,0) {
        override fun printHello() {
            println("Hi")
        }
    }, BLUE(0, 0, 0xff) {
        override fun printHello() {
            println("Bye")
        }
    }
}
```

### anotation class
annotation을 정의할 수 있다.  
아래와 같은 annotation을 이용해 정의할 수 있다.  
아래는 코틀린 공홈에 있는 예제이다.
```kotlin
@Target // 어노테이션을 지정할 타겟
@Retention // 클래스에 저장할 것인지 runtime에 반영할 것인지
@Repeatable // 같은 요소에 여러번 사용 가능하게 할 것인지
@MustBeDocumented // 문서화
```



```kotlin
@Target(AnnotationTarget.CLASS,AnnotationTarget.FUNCTION,
AnnotationTarget.VALUE_PARAMETER,AnnotationTarget.EXPRESSION)
@Retention(AnnotationRetention.SOURCE)
@MustBeDocumented
annotation class Fancy
```

아직 제대로 이해한 느낌이 아니라 나중에 제대로 이해하고 따로 글작성 해보겠다 