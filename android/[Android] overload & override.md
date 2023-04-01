# overloading vs. overriding
<br>

### 1. **overloading**
* 새로운 메소드를 정의하는 것. 과적하다라는 뜻으로 상속과는 상관이 없다. 
* 생성자의 파라미터를 다르게 하여 같은 이름의 메소드를 또 만드는 것을 말한다.

<br><br>

### 2.**overriding**
* 상속과 관련한 개념으로, 메소드의 동작만 재정의 하는 것이다. 메소드의 이름, 파라미터 모두 같아야 하며 새로운 기능을 넣는 등의 동작이 가능하다.
* kotlin 에서 오버라이딩 하려면 부모 클래스의 함수 앞에 open 키워드를 명시하여 오버라이딩 가능하도록 설정하고 자식 클래스에서 사용할 때는 override 키워드를 명시해야 한다.

<br>

~~~kotlin
open class OverRidingClass(){
			open fun ex(){}
}

class ChildClass() : OverRidingClass(){
			override fun ex() = print("override")
}
~~~