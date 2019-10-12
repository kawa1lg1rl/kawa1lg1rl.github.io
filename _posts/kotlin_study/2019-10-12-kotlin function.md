---
layout: post
title: Kotlin 함수
categories: kotlin_study
comments: true
tags: kotlin function
date: 2019-10-12
author: kawa1lg1rl
---

함수 관련 끄적인거라 설명은 거의 없음.

## 함수
### return
```kotlin
fun a(): Int = 1
fun b(): Int {
    return 1
}
```

### default params
```kotlin
fun main(args: Array<String>){
    sum() // 300
    sum(1) // 201
    sum(1,2) // 3 
    sum(b = 300) // 400
}

fun sum(a: Int = 100, b: Int = 200) {
    println( a + b)
}
```

### variadic params
```kotlin
fun main(args: Array<String>) {
    varargTest(1,2,3,4)
}

fun varargTest(vararg numbers: Int) {
    numbers.map { it ->
        println(it)
    }
}
```
```kotlin
/*
 * - output - 
 * 1
 * 2 
 * 3
 * 4 
 */
```
## 함수형 프로그래밍

### 순수 함수  
외부의 상태를 변경하지 않고 동일한 인자에 항상 같은 값을 리턴하는 함수  

### 일급 객체(First-Class Object)
함수의 인자로 전달할 수 있다.
함수의 반환값에 사용될 수 있다.
변수에 담을 수 있다.


### [일급 함수](https://developer.mozilla.org/ko/docs/Glossary/First-class_Function)
일급 객체의 성질을 띄는 함수  
익명 함수일 경우 람다식  

### 고차 함수  
함수를 인자로 받거나 함수를 리턴하는 함수


### 람다식
```kotlin
var sum:(Int, Int) -> Int = {a:Int, b:Int -> a + b} 
var sum = {a:Int, b:Int -> a + b} 
var sum:(Int, Int) -> Int = {a, b -> a + b} 

// 2중 람다식
var lambdaInLambda: () -> () -> Unit = {
    println("first lambda");
    { println("second lambda") }
}

lambdaInLambda()()


var lambdaInLambda: () -> () -> Unit = { 
    println("first lambda")
    { println("second lambda") }
}

var list = listOf(1,2,3,4)
list.map { it ->   
    println(it)
}
```


```kotlin
fun main(args: Array<String>) {
    temp(1,2, ::sum)
}

fun temp(a:Int, b:Int, c:(Int, Int) -> Int) = c(a, b)

fun sum(a:Int, b:Int): Int {
    return a + b
}
```

```kotlin
fun main(args: Array<String>) {

    var a : (String, String) -> String
            = {a, b-> "$a $b"}

}
```

### 익명함수  
람다처럼 변수선언 시 익명함수를 사용할 수 있다. 자바스크립트 같기도

### 인라인 함수  
함수 정의 시 앞에 inline 키워드를 붙여서 사용할 수 있다.
inline 함수를 코드에서 호출 시, 컴파일 과정에서 inline함수의 내용이 복붙된다고 보면된다.

인라인 함수에 람다식을 인자로 받을 경우, 람다식도 인라인 함수안에 복붙될 가능성이 있다.  
이 때 람다식 인자의 앞에 noinline 키워드를 붙이면 람다식이 inline으로 들어가지 않는다.

### 비지역 반환  
인라인 함수에 람다식을 인자로 넘길 경우, noinline 키워드를 붙이지 않았을 때  람다식에 return을 넣을 수 있다.  
이때 람다식은 인라인 함수 안에 inline으로 들어가게 되며 인라인 함수를 실행 시 return을 만나면 해당 함수를 종료한다.  
이를 비지역 반환이라고 부른다

따라서 비지역 반환을 금지하려면 crossinline키워드를 붙이면 된다.  


### 확장 함수  
특정 클래스에 내가 원하는 메서드를 추가하고 싶을때 확장함수를 사용한다.
```kotlin
fun String.getLastChar() : Char{
    return this[this.length-1]
}
```

모든 클래스에 내가 원하는 메서드를 넣고싶다면 Any에 확장함수를 추가하면 된다.


### 중위 함수  
비트연산자처럼 `3 shr 3`( 원래는 `3.shr(3)` )과 같이 사용할 수 있는 함수이다.  
함수 선언 시 `infix` 키워드를  앞에 붙이면 된다.  


### 꼬리 재귀 함수  
tailrec 키워드를 사용해 정의할 수 있다.  
재귀함수가 자신만을 호출하다 return하면 꼬리 재귀라고 볼 수 있다. 
```kotlin
tailrec fun fact(n:Int, number:Int): Int {
    return if (n <= 0) {
        number
    } else {
        fact(n-1, n*number)
    }
}

// 이건 아님
fun fact(number:Int): Int {
    if(number <= 1) number 
    else fact(number - 1) * number
}
```

### scope  
최상위 함수는 선언 순서와 관계없이 호출되지만  
지역함수는 선언 순서 상관있음.
