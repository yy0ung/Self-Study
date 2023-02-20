# 안드로이드 루퍼 & 핸들러
#### *시간이 오래 걸리는 작업일 경우, 다른 스레드에서 작업을 하고 메인 스레드로 결과를 전송한다면 안정적으로 어플을 동작할 수 있다. 이 경우 스레드간의 통신이 필수적이며, 스레드 간 통신을 돕는 것이 루퍼와 핸들러이다.*
<br>

### 1. **루퍼 Looper**
* 하나의 스레드에는 하나의 looper가 있다. (1:1 관계)
* 안드로이드에서 기본적으로 MainActivity가 실행되면 자동으로 메인 스레드의 looper가 돌기 시작한다. 
* 각 스레드의 looper에는 MessageQueue 가 존재하는데, 해당 스레드가 처리해야 하는 동작들이 Message 형태로 하나씩 쌓이게 된다. 
* Looper는 궁극적으로 MessageQueue에 들어오는 메세지를 하나씩 꺼내어 적절한 Handler로 전달하는 역할을 한다. 
  * 어떤 handler에 메세지를 전달해야 하는지에 대한 참조를 각 looper가 가지고 있다. 
* 이름이 looper인 이유는 메세지 큐가 비어있을 때는 아무 동작도 하지 않고 무한 루프만 돌고, 루프를 돌면서 메세지가 쌓이면 전달해주기 때문이다. 

<br><br>

### 2. **핸들러 Handler**
* 특정 메세지를 looper의 메세지 큐에 넣거나, looper가 메세지 큐에서 특정 메세지를 꺼내어 전달하면 처리하는 기능을 수행한다. 

<br>

* looper로 메세지를 전달하는 경우
  * Message 객체를 생성 → 전달.
  * sendMessage() 를 통해 Message를 적재.
  * post로 시작하는 메서드를 통해 Ruunable 객체를 직접 적재 가능.

<br>

* looper로부터 메세지를 전달받는 경우
  * Runnable 객체가 담겨있다면 해당 객체의 run()메서드를 호출하여 작업을 실행
    * Runnable 객체는 인자, 리턴값이 없고 예외를 발생시키지 않는다. 값을 리턴하는 것이 아니라 내부의 run 함수를 실행시킨다.
  * Message 객체가 담겨있다면 Handler가 가지고 있는 handleMessage()를 호출해서 해당 Handler가 메세지를 전달받는다.
  * *Runnable 객체는 run 자체가 그 동작 자체를 의미하지만 Message 객체는 동작에 대한 정보이기 때문에 Handler가 실행해줘야 함.*

<br><br>

### 💡 **예제**

<br>

- A Thread → B Thread로 객체를 보내고 싶음
- A 는 B가 가진 handler의 sendMessage(), post 메서드를 이용해서 원하는 객체를 보낸다.
- B는 Handler가 A로부터 전달받은 메세지를 B의 MessageQueue에 넣는다.
- B의 Looper는 MessageQueue에 담긴 작업을 순차적으로 Handler에 보내 작업 수행을 시킨다.
- B의 Handler는 looper에게서 받은 작업 (큐 안에 있던 메세지)을 handleMessage() 등을 통해 수행한다.

<br>

~~~kotlin
var hanlder : Handler? = null
val thread = Thread {
	handler = Handler(Looper.getMainLooper())
}
thread.start()
~~~

<br>

*→ 메인스레스와 다른 스레드의 상황에 대입해보자면, 메인스레드가 가지고 있는 Looper의 MessageQueue에 다른 스레드의 결과를 담아두면, 메인 스레드의 Handler가 차례대로 이를 수행한다. (Handler는 looper와 queue가 있어야 하기 때문에 무조건 Looper가 필요하다.)*

<br><br>

다른 스레드에서 UI 변경 작업을 처리하는 예시 코드

~~~kotlin
class MainActivity : AppCimpatActivity(){
	
	private lateinit var title : TextView
	private lateinit var handler : Handler
	
	override fun onCreate(savedInstanceState : Bundle?){
		super.onCreate(savedInstanceState)
		setContentView(R.layout.activity_main)
		
		title = findViewById(R.id.tv)

		//Main Thread Handler
		handler = Handler()
		
		val timerThread = TimerThread()
		timerThread.start()
		
		stopButton.setOnClickListener{
			timerThread.stopRunning()
		}

	}
	
	inner class TimerThread : Thread(){
		private var time = 0
		private var isRunning = true

		override fun run(){
			super.run()
			while(isRunning){
				sleep(1000)

				handler.post{
					title.text = "timer thread run ${time} sec"
					time++
				}
			}
		
		handler.post{ title.text = "timer thread stopped." }
		
		}

	}
	
	fun stopRunning(){ isRunning = false }
}
~~~