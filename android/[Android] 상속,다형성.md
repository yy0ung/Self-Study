# 상속, 다형성

<br>

### 1. 추상화

- 객체지향에서 의미하는 추상화는 객체의 공통적 속성과 기능을 추출하여 정의하는 것을 의미.
- 예를 들어, 자동차와 자전거는 세부적으로는 다른 속성을 가질 수 있지만, `이동수단` 이라는 공통적인 특징을 추출하여 정의할 수 있음.
- 추상화는 `abstract class (추상 클래스)`, `Interface (인터페이스)` 로 구현이 가능함.

<br>

- 추상클래스
    - 대략적인 설계의 명세와 공통 기능을 구현한 클래스. 상속받는 하위 클래스는 이 추상성을 구체화하여 사용해야 함.
    - `abstract` 키워드로 클래스를 정의하고, 초기값을 가지는 일반 속성을 선언할 수 있음.
    - 하위 클래스에서 재정의하여 사용하고 싶은 경우 `abstract` 키워드를 사용.
    
    ```kotlin
    abstract class Example(){
    	// 초기값을 가지는 변수 선언 가능
    	val initVal = "possible"
    
    	// 일반 메서드도 선언 가능
    	fun method1(){ println("\n") }
    	
    	// 하위 클래스에서 반드시 재정의 해야 함.
    	abstract var value1 : Int
    	abstract fun method2()
    }
    ```
<br>

- 인터페이스
    - 추상 메서드나 상수를 통해서 **어떤 객체가 수행해야 하는 핵심적인 역할만을** **규정**해두고, **실제적인 구현은 해당 인터페이스를 구현하는 각각의 객체들에서 하도록** 프로그램을 설계하는 것.
    - 인터페이스에는 “역할”  을 정의하고, 각각의 구현체들에서 “구현” 하는 것. 객체지향 프로그래밍은 이 역할 정의와 구현을 분리시키는 것이 핵심이며, *인터페이스는 역할을 정의하는 부분을 추상화.*
    - `abstract` 키워드는 사용하지 않음.
    - 코틀린에서는 interface 를 사용해야 다중 상속이 가능.
    
    ```kotlin
    interface Example {
    	val value1 : Int // 추상
    	fun method1() // 추상
    	fun method2() { println("\n") } // 일반
    }
    ```

<br><br>

### 2. 상속

- 기존의 클래스를 재활용하여 하위 클래스에서 상속받아 사용하는 것.
    - 하위 클래스는 상위 클래스의 생성자를 호출해야 함.
- kotlin 에서는 기본 class 는 상속 불가능. 반드시 아래 두 키워드 중 하나를 포함해야 상속이 가능.
- `open`
    - 상속해줄 수 있는 키워드로, 부모가 구현한 함수를 그대로 사용하거나 override 해서 사용.
    - 상속 받는 대상이 없어도 인스턴스화 가능.
    - overriding
        - 상속과 관련한 개념으로, 메소드의 동작만 재정의 하는 것이다. 메소드의 이름, 파라미터 모두 같아야 하며 새로운 기능을 넣는 등의 동작이 가능하다.
        - kotlin 에서 오버라이딩 하려면 부모 클래스의 함수 앞에 open 키워드를 명시하여 오버라이딩 가능하도록 설정하고 자식 클래스에서 사용할 때는 override 키워드를 명시해야 한다.
- `abstract`
    - 하나 이상의 abstract function, 요소가 있을 경우 abstract 로 선언해야 함.
    - 상속받는 대상은 abstract 요소를 반드시 구현해야 함.
    - 상속 받는 대상이 없으면 인스턴스화 불가능.
- 타입 캐스트
    - 상속에서 부모와 자식 클래스는 서로 up casting 과 down casting 이 가능.
    
    ```kotlin
    // 부모 클래스 : A
    // 자식 클래스 : B
    
    if (A is B) {
    	// 이 안에서 자식 클래스인 B 로써 동작
    } // 나오면 다시 A 로 동작
    
    A as B
    // 이후로 B 로 동작
    ```
    
<br>

- 인터페이스와 추상클래스로 하는 상속
    - 상속의 경우 **상위 클래스의 속성과 기능들을 하위 클래스에서 그대로 받아 사용하거나 오버라이딩을 통해 선택적으로 재정의하여 사용**
    - 인터페이스를 통한 구현은 반드시 **인터페이스에 정의된 추상 메서드의 내용이 하위 클래스에서 정의**되어야 함.
    - 인터페이스가 역할에 해당하는 껍데기만 정의해두고, **하위 클래스에서 구체적인 구현을 하도록 강제**하는 것에 비해, 상속 관계의 경우 상황에 따라 모든 구체적인 내용들을 정의해두고 하위 클래스에서는 그것을 단순히 가져다가 재사용.
    - ***추상화 정도 : 인터페이스 > 추상클래스 이용한 상속***
    
<br><br>

### 다형성

- **어떤 객체의 속성이나 기능이 그 맥락에 따라 다른 역할을 수행할수 있는 객체 지향의 특성**
- 같은 이름인데, 상황에 따라 다른 기능을 하는 것이 다형성의 핵심
    - 이러한 이유 때문에 오버라이딩과 오버로딩이 다형성의 종류가 됨.
    - 둘 모두 같은 이름이지만 다시 정의되어 다른 역할을 하기 때문.
- 상위 클래스의 참조 변수로 하위 클래스의 객체를 참조할 수 있는 것.
    - 예를 들어, `Vehicle` 클래스가 `Car`, `Bike` 클래스의 부모 클래스. 이러한 `Vehicle`들의 배열을 만들고 싶을 때, `Car`, `Bike` 는 그 자체로는 다른 이름을 가지고 있기 때문에 만들 수 없음. 이때 `Vehicle` 를 타입으로 하는 배열을 만들면 자식 클래스들이 모두 추가될 수 있음.


<br><br>

### Sealed class

- 자기 자신이 추상클래스이며 자신을 상속받는 여러 자식 클래스를 가질 수 있음.
    - 자식 클래스는 같은 파일 안에만 선언되어야 함.
    - `private` 생성자만 가지게 됨.
- 인스턴스화 불가능
    - 추상 클래스이기 때문에 직접 인스턴스화 불가능.
    - 하위 클래스로 상속하고 그 하위클래스를 인스턴스화 할 수 있음.

```kotlin
sealed class Result
data class Success(val data: String) : Result()
data class Error(val message: String) : Result()

// (잘못된 예시) 직접 인스턴스화가 불가능
// val result = Result()

fun processResult(result: Result) = when (result) {
    is Success -> println("Success: ${result.data}")
    is Error -> println("Error: ${result.message}")
}

val successResult = Success("Data loaded successfully")
val errorResult = Error("Error while processing data")

processResult(successResult) // 출력: Success: Data loaded successfully
processResult(errorResult)  // 출력: Error: Error while processing data
```