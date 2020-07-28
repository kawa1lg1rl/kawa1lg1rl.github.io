

* internal 접근제어자  
 같은 모듈에서만 접근 가능  
 다른 클래스에서 internal이 붙은 클래스의 객체를 생성할 때에는 객체에도 internal을 붙여줘야함.  
 변수나 메서드에도 internal 적용 가능 

* 생성자에도 접근제어자 가능

* 연관 의존 집합 구성 관계

* getter/setter
    * getter/setter 오버라이딩 가능.
```kotlin
var string: String? = null
    get() {
        if(field == null) {
            return "123"
        } else {
            return field
        }
    }
```

* 지연 초기화  
    * lateinit키워드를 붙여서 사용한다.  
클래스의 프로퍼티 같은 경우, null값을 허용하지 않는다. (따라서 null값을 넣을떄는 ?을 붙여주게된다.)
원시 타입만 가능, var만 가능  
    * lazy키워드는 lateinit의 val버전
        * lazy와 by lazy는 다름

* Delegates
    * by
    * observable
    * vetoable


* object
    * 싱글톤으로 사용가능
    * 클래스 지정하지 않고 사용 가능
    
* 제네릭
    * T 
        ```kotlin
        // 아래 둘 처럼 사용 가능
        class MyClass<T> where T:interfaceA, T:interfaceB
        fun <T> myMax(a: T, b: T) : T where T:Number, T:Comparable<T> {

        }
        ```

* 자료형과 클래스
    * Int는 자료형이자 클래스
    * String도 자료형이자 클래스
    * String?은 자료형
    * Array<String>도 자료형

* 가변성, 검색해봐야함
    * 공변성
        * out
    * 반공변성
        * in
    * 무변성

* reified 연산자 


* Class<T>, KClass<T>
    * K Class : Object::class
    * Class : Object::class.java (자바에서의 Class와 같음)

* 다차원 배열일때 deepToString 쓰면 아래 배열까지 toString됨

* Array()로 배열 생성시,size, init을 파라미터로 받음.
    * init에는 초기값을 넣어야하며 람다식을 사용함.

* 메서드 체이닝

* flatten : 다차원배열 평탄화 


* StringBuilder 
    * 스트링빌더를 쓰면 `s[1] = 'b'`와 같은 식의 변경이 가능함.]
    * 또한 append insert delete 메서드를 이용해 쉽게 문자열 다루기 가능 

* trimMargin
    * 특정 문자 기준으로 공백제거 가능
    * 기본값은 `|` 