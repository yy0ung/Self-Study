# 안드로이드 lateinit & by lazy
<br>

### 1. **lateinit**
* Primitive Type 에 대해서는 사용 불가 (int, long, double, float)

<br>

~~~kotlin
lateinit var x : String
x = "start"
println(x)
~~~

<br><br>

### 2. **by lazy**
* 사용될 때 초기화 됨.
* 초기화 시점을 조정할 수 있고, 값이 by lazy 를 통해 지연 생성되어 호출될 때 생성되게 한다.

<br>

~~~kotlin
lateinit var inpultValue : String
val x : Int by lazy { inputValue.length }
inputValue = "start"
// 여기서 사용됨.
println(x)
~~~