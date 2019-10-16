---
layout: post
title: Kotlin sequence
categories: kotlin_study
comments: true
tags: kotlin sequence
date: 2019-10-15
author: kawa1lg1rl
---


## 시퀀스
java의 stream과 비슷하다고 한다.  
뭔지 잘 모르겠다.  

사용법은 아래와 같다.

### 사용법

```kotlin
var nums = generateSequence(1) { it * 2}

println(nums.take(10).toList())
```
위의 코드는 초기값 1을 시작으로 2씩 곱하는 코드이다.  
`toList`를 진행할때 결과가 정해진다고 한다.  
이해가 잘 가지 않아 예제를 더 살펴보았다.  

`List`를 `sequence`로 바꾸어 연산하는 예제이다.   
우선 아래와 같은 코드가 있다.
```kotlin
    var list = listOf(1,2,3,4,5)
    
    println(list.
    map {
        println("map $it");
        it
    }.filter {
        println("filter $it");
        it < 4
    })
```
결과값은 아래와 같다.
```
map 1
map 2
map 3
map 4
map 5
filter 1
filter 2
filter 3
filter 4
filter 5
[1, 2, 3]
```

이 코드에서 `list`를 `sequence`로 바꾸었다.

```kotlin
    var list = listOf(1,2,3,4,5)
    println(list.asSequence().map {
        println("map $it");
        it
    }.filter {
        println("filter $it");
        it < 4
    }.toList())
```

`println`의 `list`에 `.asSequence()`가 추가되었고, `filter`의 결과값에 `toList`가 추가되었다.  
결과값은 아래와 같다.

```
map 1
filter 1
map 2
filter 2
map 3
filter 3
map 4
filter 4
map 5
filter 5
[1, 2, 3]
```

`map`의 결과(`List`)를 생성하지 않고 바로 `filter`를 거치면서 `toList`할 때 최종적으로 결과물을 만들어 낸 것이다.  

이를 `Lazy evaluation`이라고 하는데,   
`asSequence`를 하지 않은 코드가 `Eager evaluation` 방식으로 작성되었고,  
`asSequence`를 한 코드가 `Lazy evaluation` 방식으로 작성되었다.  
`Lazy evaluation`에 대해서는 아직 정확히 이해가 가지 않아 `Sequence` 사용법만 알고 넘어가기로 했다.


`Lazy evaluation` 방식으로 돌아가는 특별한 `Collection`이라고 생각하면 될 것 같다.. 
