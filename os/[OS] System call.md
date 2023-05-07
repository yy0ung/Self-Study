# OS 시스템 콜 System Call

<br>

### 1. **시스템 콜**
* 어플리케이션이 hw를 바로 (직접) 제어하지 못하도록 기능을 요청하는 통로를 system call이라고 함. 
* 커널이 제공하는 기능들 중에서 사용자가 사용할 수 있는 것을 모아둔 것들.

<br>

💡 printf()라는 api 를 예시로 보면, 해당 api 가 실행될 때 user 모드에서 kernel 모드로 넘어가면서 그 진입점에 있는 코드가 system call (그때 수행되는 함수). 
<br>
💡시스템 콜은 실제로 커널 request 하는 것으로 API 와는 다르다. malloc(), calloc(), free() 등의 APIs 는 brk() 라는 system call 을 담은 container 라고 할 수 있다. 

<br>

* 시스템 콜의 유형
  * 프로세스 제어
  * 파일 조작
  * 장치 조작
  * 정보 유지 보수
  * 통신과 보호

<br>

* 시스템 콜 쓰는 이유 (명분)
  * Easy to program : 없다면 모든 코드를 매번 다 짜야함.
  * Increasing system security
  * Increase program portability : 표준화의 중요성

<br><br>

### 2. **API (응용 프로그래밍 인터페이스)**
* 엄청난 양의 시스템 콜이 수행되는데, 사용자의 대부분은 그 과정에 대해 알지 못한다. 
* 대부분의 개발자들을 API 를 통해 프로그램을 설계한다.
* 즉 시스템 콜 인터페이스는 사용자가 호출한 API 함수의 호출을 가로채어 필요한 시스템 콜을 부른다. 개발자는 시스템 콜이 어떤 과정을 처리하는지에 대해서는 알 필요가 없다. API 를 적절하게 사용하는 것에 신경쓰면 된다. 