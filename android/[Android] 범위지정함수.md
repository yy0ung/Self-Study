# 안드로이드 Scope Functions
<br>

### 1. **Scope Functions 개념**
* 범위지정함수는 다른 함수를 인수로 사용하는 고차함수이다. 
* 특정 객체에 대한 작업을 블록 안에 넣어서 실행하게 하는 함수로 해당 블록은 작업의 범위가 된다. 해당 함수를 호출하면 블록으로 임시 범위가 형성되어 해당 범위 안에서 이름 없이 객체 접근이 가능해지는 것이다.

<br><br>

#### *예시 객체*
~~~kotlin
data class Sample(
	var title : String = "",
	var cnt : Int = 0
){
	fun check() : Boolean = cnt>5
}
~~~

<br><br>

### 2. **Scope Functions 종류**
* **let**
  - 객체를 받아 작업하고 마지막 줄을 반환할 때 사용.
  - 객체에 접근할 때 it을 사용.
  - null check 가 필요한 경우, null 이 아닐 때만 수행되는 블록을 만드는 경우 let을 사용한다.
  - let 블록 안의 it 은 nullable 하지 않다.

<br>

~~~kotlin
fun main(){
	var sample : Sample? = null
	var isNull = sample?.let { it -> notNull(it) }
}
~~~

<br>

* **also**
  - 수신 객체 자신을 반환한다.
  - also는 객체의 요소를 수정하고 추가적인 작업을 하고 반환할 경우 사용한다.
  - let 와 같이 객체에 접근할 때 it을 사용한다.

<br>

~~~kotlin
var cnt = 1;
var sample = Sample("test", 5)

fun getCnt() = cnt.also{
	cnt++
}

fun getNextCnt() = sample.also{
	sample.cnt = it.cnt + 1
}

fun main(){
	print("${getCnt()}")
	print("${getCnt()}")
	print("${getNextCnt()}")
	print("${getNextCnt()}")
}

// 출력값
// 1
// 2
// 6
// 7

// getCnt() 는 cnt를 반환하는 함수로 반환하고 → 1을 더하고 → 다시 반환 → 1을 더하는 플로우 이기 때문에 출력값이 1,2 로 나온다.

// getNextCnt() 는 블록 안에서 객체의 cnt를 바꿔버린 것이기 때문에 바뀐 값이 출력된다. 따라서 해당 값을 getCnt()처럼 출력하려면 copy를 사용해야 한다. 
~~~

<br>

* **apply**
  * 객체 내부 요소를 변경하고 객체 자체를 반환하는 함수

<br>

~~~kotlin
// use apply
val sample = Sample().apply{
	title = "apply test"
	cnt = 5
}

// do not use apply
val sample = Sample()
sample.title = "apply test"
sampe.cnt = 5
~~~

<br>

* **run**
  * apply 와 동작은 비슷하지만 객체 대신 run 블록의 마지막 줄을 반환하는 함수. 

<br>

~~~kotlin
val sample = Sample("run test", 5)
val check = sample.run{
	cnt = 10
	check()
}

// return 값이 check()
// true 가 return 됨.
~~~

<br>

* **with**
  * run과 똑같이 동작하지만, with은 객체를 파라미터로 받아야 한다.

<br>

~~~kotlin
val sample = Sample("run test", 5)
val check = with(sample){
	cnt = 10
	check()
}

// return 값이 check()
// true 가 return 됨.
~~~