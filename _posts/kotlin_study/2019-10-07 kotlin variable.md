---
layout: post
title: \[Kotlin\] 변수
categories: kotlin study
comments: true
tags: kotlin variable
date: 2019-10-08
author: kawa1lg1rl
---

## 코틀린 변수

코틀린의 변수와 관련되어 적어놓은 문서  
현재 문서에서 나오는 내용 중 일부는 따로 적어서 업로드할 것

### 기본형과 참조형
코틀린의 모든 변수는 참조형으로 작성된다. [참조형과 기본형](https://en.wikipedia.org/wiki/Value_type_and_reference_type)(해당 문서에서는 `value type`과 `reference type`으로 구분한다.)

기본형의 경우 `c`나 `java`에서 볼 수 있는 `int`, `double`, `float`, `boolean` 같은 자료형  
참조형의 경우 `포인터`, `객체`같은 자료형


### 자료형
 * `Byte` : 정수 1바이트
 * `Short` : 정수 2바이트
 * `Int` : 정수 4바이트 
 * `Long` : 정수 8바이트
 * `Boolean` : 참/거짓
 * `Char` : 문자
 * `String` : 문자열




### 코틀린 변수 선언
코틀린은 변수를 아래와 같이 선언할 수 있다.
```kotlin
var a = 1
var b:Int = 1
var c:Long = 1
val d = 1
val f:Int = 2
val g:Int
```
코틀린의 경우에는 `var`와 `val`을 이용해 변수를 선언할 수 있다.  
`var`의 경우에는 변수의 값을 변경할 수 있지만, `val`의 경우에는 변경할 수 없다.  
자바의 `final`이라고 생각해도 될 것 같다.  
변수를 선언함과 동시에 초기화하지 않는다면 `g`변수처럼 자료형과 함께 선언해야 한다.

### 변수 최소,최대값
```kotlin 
Long.MAX_VALUE
Long.MIN_VALUE
```

### 문자열 표현식

#### $
php를 예전에 아주 잠깐 해봤던 적이 있는데 kotlin의 경우 php와 비슷한 점이 있었다.  
문자열에 `$`을 넣어 값을 문자열에 표현하는 방식이다.

```kotlin
var a = 1
println("a is $a") 
// out: a is 1

fun test(): Int {
    return 123
}
println("test() return : ${test()}") 
// out: test() return : 123
```

`$`을 출력하고 싶을때는 `$`을 사용하거나 `\`을 사용하면 된다. 
```kotlin
println("test : \$ or ${'$'}")
```

`$`을 사용하여 `'`, `"`, `$` 등의 문자를 표현할 수 있지만, `\`를 사용하는게 편한거 같다.

### 다중 문자열
파이썬에서 사용하던 것과 같이 `"""`를 이용하여 multiline string을 표현할 수 있다.

```kotlin
var testString:String = 
"""string1
string2"""
```

`"""`를 사용하면 문자열 안에 더블쿼터 사용시 `\`를 붙이지 않아도 된다.  

### alias
```kotlin
typealias testString = String

var a:testString = "debug mode"
println(a)
```


### Null Check
Null Check라고 하였지만 Check라는 말이 맞을지 모르겠다.  
```kotlin
var a:String? = null
var b:String = "123"
b = null // Error
```
코틀린에서는 자료형 뒤에 `?`를 붙이는 것으로 `null` 값을 넣을 수 있을지 없을지를 결정할 수 있다.  
변수 `a`와 같이 `?`을 붙인 경우에는 `null`을 넣을 수 있다.  
하지만 `b`와 같이 붙이지 않았을 경우 `null`을 넣을 수 없다.  

### Non-null assertion, Safe call
`null`을 넣을 수 있는 변수를 사용 시, `!!`과 `?`을 이용할 수 있다.  
> `!!`(non-null assertion)을 이용하는 경우
```kotlin
fun main(args: Array<String>) {
    var a = test()

    a!!.map {
        println(" :: $it")

    }
}

fun test(): List<Int>?{

    var temp:List<Int>? = listOf() // nullable variable

    temp = temp!!.plus(1) // non-null assertion
    temp = temp!!.plus(3)
    temp = temp!!.plus(5)
    return temp
}
```
```kotlin
/*
* - output - 
* :: 1
* :: 3
* :: 5
*/
```

`List 타입의 변수 temp` 를 선언할 때 `?` 을 붙여주었다.  
이후 `temp`에 값을 추가하기 위해 `plus` 메서드를 사용했다.  
하지만 `temp.plus()`와 같이 사용 시 에러가 난다.  
따라서 `이 변수는 현재 null이 아니다`라는 의미로 `!!`을 붙여준다.  
> `temp!!.plus(1)`  

또한 `test`메서드의 결과값(`List`)를 `a`변수에 받아와 `map`을 이용해 값을 출력한다.  
이 때도 `test`메서드의 `return type`이 `List<Int>?`이기 때문에 `!!`을 붙여줘야만 한다.  
  
`!!` 대신 `?`(safe call)을 이용할 수도 있다.  
```kotlin
fun main(args: Array<String>) {
    var a = test()

    a?.map {
        println(" :: $it")
    }
}

fun test(): List<Int>?{
    var temp:List<Int>? = null

    temp = temp?.plus(1) 
    temp = temp?.plus(3)
    temp = temp?.plus(5)

    return temp
}
```
```kotlin
/*
* - output - 
*/
```

`temp`변수에 `null`이 들어갔다.  
`!!`이 전부 `?`으로 대체 되었다.
`?`은 `!!`과 달리 `null일 수도 있다.` 라는 의미이다.  
따라서 `temp?.plus(1)`의 경우에 `temp가 null일 수도 있으니 null일 경우 아무것도 하지마라`라는 의미로 해석할 수 있다.  
  
실제로 코드에서 `temp`가 `null`이기 때문에 아무런 값도 더해지지 않았고  
`a`의 경우에도 `map`을 돌리는데 `a`의 값이 null이기 때문에 아무것도 실행되지 않았다.



### Elvis operator
`?:`이라는 연산자이다.  
`삼항 연산자`의 `null 체크` 버전이라고 생각하면 쉽다.

```kotlin
var a:String? = null

...
...

println(a ?: "a is null")
```
위 코드의 println 줄을 보면 
`a ?: "a is null"`이라는 코드가 있다.  
a의 값이 `null`이 아닐 경우 a의 값을 출력하고,  
a의 값이 `null`일 경우 `"a is null"`이라는 문자열을 출력한다.

또한 삼항 연산자처럼 사용할 수 있는 것이 있다.
```kotlin
var a = 1
var b = if(a > 0) a else -1
```
`a`가 `0`보다 크면 `b`에 `a`를 넣고 아니라면 `-1`을 넣는다.


### `==` , `===`
코틀린은 자바의 `isEquals`와 같은 메서드를 사용할 필요가 없다.
```kotlin
var a:String = "123"
var b:String = "123"

println( a == b ) // true
```

그냥 `==`을 사용하면 된다.  
또한 자바스크립트나 php처럼 `===`을 사용할 수도 있다.  
`===`을 이용할 때는 참조주소를 비교할 수 있다.
  
`String`은 같은 문자열로 초기화 해주었을 경우 참조 주소가 같다. 
```kotlin 
var a = "123"
var b = "123"
a === b // true

a = a + "4"
a === b // false
```

### `Any` type과 `is` 연산자
`Any`라는 자료형이 있다.  
어떠한 자료형도 나타낼 수 있다.
```kotlin
fun main(args: Array<String>) {

    var a:Any
    a = 1 // Int로 캐스팅됨
}
```
또한 `Any`타입으로 선언된 변수는 자료형을 바꿀수 있다.
```kotlin
var a:Any = 1
a = "123"
println(a)
```

아래는 자료형을 비교할 수 있는 `is`연산자와 관련된 코드이다.
```kotlin
fun main(args: Array<String>) {

    var a = test() // a is Short

    if( a is Int ) {
        println("a is Int")
    } else if( a !is Int){ 
        println("a is not Int")
    }
}

fun test(): Any {
    var b: Short = 1 
    return b // return Short
}
```
```kotlin
/*
 * - output -
 * a is not Int
 */
```


### `as` 연산자
`as`는 캐스팅을 위한 연산자라고 봐도 무방하다.  
c언어에서는 아래와 같이 형변환을 한다. `(char*)`
```c
char *p = (char*)malloc(0x10) 
```

이 형변환 하는 것을 kotlin에서는 as로 사용할 수 있다.
```kotlin
var a: Byte = 10
var b: Int = a as Int
```

### 비트연산자
c언어처럼 `|`, `&`, `~`, `>>`, `<<`, `^` 을 이용할 수 없다.
대신 아래와 같은 함수를 사용할 수 있다.
```kotlin
var a = 0b_00001111
a.shl(2)  // << 
a.shr(2)  // >>
a.ushr(2) // 부호없는 >>
a.and(2)  // &
a.or(2)   // | 
a.xor(2)  // ^
a.inv()   // ~
```
또한 위의 연산자들은 `a shl 2`와 같이 사용할 수 있다.


### 그 외 연산자
산술, 논리, 비교, 대입 연산자는 c언어나 자바와 거의 같다.  
