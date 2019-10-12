---
layout: post
title: Kotlin Loop
categories: kotlin_study
comments: true
tags: kotlin Loop
date: 2019-10-12
author: kawa1lg1rl
---

## for문

### java의 for문

```java
for(int i = 0; i<10; i++) {
    //
}
```

### kotlin의 for문
```kotlin
for(i in 0..9) {
    // 0부터 9까지 1씩 증가
}


for(i in 0..9 step 2) {
    // 0부터 9까지 2씩 증가
}

for(i in 9 downTo 0) {
    // 9부터 0까지 1씩 감소
}

for(i in 9 downTo 0 step 2) {
    // 9부터 0까지 2씩 감소
}
```

## while문
c나 java와 같다

## do~while 
c나 java와 같다

## Label을 이용한 Loop Break
라벨을 이용하면 break시 원하는 블록을 지정할 수 있다.(return, continue도 가능.)
```kotlin
@first for(i in 1..9) {
    println(i)
    @second for(j in 1..9) {
        if(i > 4 ) break@first
    }
}
```

```kotlin
/* - output -
 * 1
 * 2
 * 3
 * 4 
 * 5 
 */