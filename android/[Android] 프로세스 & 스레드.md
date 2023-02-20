# 안드로이드 프로세스 & 스레드
<br>

### 1. **프로세스 Process**
* 한 프로그램의 하나의 task를 말한다. 1개의 프로그램이 1개의 프로세스에 해당한다고 쉽게 설명할 수 있다. 
* 프로세스의 메모리 영역은 code, data, heap, stack 등의 영역으로 나눌 수 있다. 
* 각각 영역들을 따로 가지고 있기 때문에 context switch 문맥교환이 일어나면 교환 비용이 높다.

<br><br>

### 2. **스레드 Thread**
* 한 프로세스 내에 작동하는 실행 흐름으로 프로세스의 대부분 영역을 공유한다. 대부분을 공유하고 있기 때문에 문맥교환의 비용이 낮다.
* 시간이 오래 걸리는 어떤 작업을 한 스레드에 모두 넣어두면 작업이 완료될 때까지 앱 전체가 응답하지 못한다. → 특정 작업은 특정한 스레드에 넘겨서 처리하는 방식이 쓰인다.  *(백그라운드 스레드 사용)*
* 원칙적으로 메인 UI 스레드 외의 다른 스레드는 UI요소에 접근할 수 없다.
  * 이유? 여러 스레드에서 텍스트를 변경하는 상황이 발생하면 혼란이 올 수 있기 때문이다. 동작의 무결성을 보장하기 위해 타 스레드에서는 UI 를 건드릴 수 없고 메인에서만 접근 가능하게 한다.

<br>

* 별도의 스레드를 생성하는 방법
  * thread 클래스를 상속하는 새로운 클래스를 만들어서 run 메서드를 오버라이드하고, 해당 스레드를 start 메서드를 이용해서 실행한다.
  * Runnable 인터페이스를 사용하여 실행.

<br>

~~~kotlin
class MainActivity : AppCompatActivity(){
	override fun onCreate(savedInstanceState: Bundle?){
		super.onCreate(savedInstanceState)
		setContentView(R.layout.activity_main)
		
		//Thread() 클래스
		var thread1 = NewThread()
		thread1.start()

		//Runnable 인터페이스
		var thread2 = Thread(NewThread2())
		thread2.start()

		//내부에 메서드가 하나만 있는 경우 람다식으로 변환도 가능.
		Thread{
			//thread에서 실행되는 코드
		}.start()

	}
}

class NewThread1 : Thread(){
	override fun run(){
		//thread 에서 실행되는 코드
	}
}

class NewThread2 : Runnable {
	override fun run(){}
}
~~~

<br>

  *-> 이 두 방법은 상속 vs 인터페이스 의 차이.*