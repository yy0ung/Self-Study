# 안드로이드 GC & 참조

<br>

### 1. **GC (가비지 컬렉터)**
* 개념
  * garbage collection 은 메모리 관리 기법 중 하나로 프로그램이 동적으로 할당했던 메모리 영역 중 필요없게 된 영역을 해제하는 기능. 프로그램을 실행하다가 메모리가 부족해지는 순간이 오면 추가적으로 메모리를 더 요청하는데, 이때 GC 가 실행됨.
  *  GC 를 지원하지 않으면 메모리를 할당한 후 수동으로 해제까지 직접 해 줘야 한다. 해제하지 않으면 메모리 누수가 생기거나 메모리를 다시 사용하는 등 버그가 날 수 있다. 
      *  JVM 기반의 자바, 코틀린은 JVM 내의 GC 가 불필요한 메모리를 정리한다. 

<br>

* 동작방식
  - Stop The World
    - GC 가 수행될 때 전체 어플리케이션이 멈추는 단계
    - 수행 스레드 제외 모든 스레드가 작업을 멈추고 GC 후에 작업을 재개한다.
    - 메모리를 재배치하고 있는데 메모리 사용하면 안되니까 멈추는 것.
  - Mark and Sweep
    - Mark : GC의 대상을 판별
    - Sweep : Mark 된 메모리를 해제

<br>

* *더  이상 사용하지 않는 객체에 대한 참조는 유지하면 안된다.*
  * companion object 는 어플이 실행되는 동안 GC 의 대상이 되지 않기 때문에 무거운 객체를 참조하고 있으면 메모리 누수가 발생한다. 
  * 더이상 필요하지 않은 객체에 null 을 할당한다. 할당된 메모리를 해제하는 명시적 함수가 없기 때문에 null 로 선언하여 다음 GC 의 대상으로 만든다. 

<br><br>

### 2. **참조**
#### *primitive type (기본타입), reference type (참조타입)*

* 기본타입은 stack에 직접 값을 가지고 있고 참조타입은 heap 영역의 객체 주소를 stack 영역에 가지고 있다. 
* 주소값을 가지게 되는 것이 참조, 이때 가지고 있는 변수가 참조변수, 주소값이 참조값.

<br>

~~~java
class A {
	public int myId;
    
    A(int myId) {
    	this.myId = myId;
    }
}

A a = new A(4); // a - 참조변수, a 가 가지고 있는 것이 주소값

A b = a; // b - 참조변수, a와 같은 주소값 가지게 됨.

b.myId = 5; // b 는 a와 가리키는 주소가 같음. 그 값을 바꾸는 것

System.out.println(a.myId); //5
~~~