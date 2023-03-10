# OS Interrupt

<br>

#### *예상치 못한, 외부에서 발생한 이벤트. 하드웨어 및 소프트웨어가 특정 업무를 수행하기 위해 CPU에게 보내는 신호.*

<br>

### **1. Interrupt 종류**
* 하드웨어 인터럽트
  * CPU 외부로부터의 요청에 의해 발생하는 인터럽트
  * I/O, 전원 이상, 외부 신호 등이 있다.
* 소프트웨어 인터럽트
  * 잘못된 명령이나 잘못된 데이터를 사용한 경우.
  * 프로그램의 오류로 발생하는 인터럽트
  * Divided by zero, Overflow/Underflow 등이 있다.

<br><br>

### **2. Interrupt 과정**
#### *인터럽트 발생하면 프로세스를 중단해서 처리해줌.*

<br>

* 인터럽트를 발생시키고 CPU 는 현재 실행 중이던 코드까지 실행한다.
* 수행 중이던 프로세스의 상태를 PCB 에 저장하고, 다음 실행할 주소는 PC (Process Counter) 에 저장한다.
* 인터럽트 벡터를 읽고 ISR (interrupt Service Routine) 주소값을 얻어 ISR으로 점프하여 루틴을 실행.
* 해당 작업을 처리하고 완료되면 프로세스의 상태를 복구한다.
* 중단했던 프로세스를 다시 실행한다.