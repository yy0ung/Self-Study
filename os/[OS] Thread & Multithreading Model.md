# OS Thread & Multithreading Models
<br>

### 1. **Thread overview**
* 프로세스 내부에는 최소 하나의 스레드가 존재한다. 
* 프로세스는 리소스 영역과 제어 영역이 있는데, 스레드는 제어하는 영역에 해당한다. 
  * 메모리 관점에서 보면, 같은 프로세스의 스레드들은 동일한 주소 공간을 공유함. 그 안에서 일정 부분을 각 스레드가 가지고 있음. 
  * 원래는 자원과 제어를 모두 가지고 있어야 되는데, 스레드는 자원은 공유하고 제어 부분만 많이 가지고 있어서 Light Weight Process에 해당함. (프로세스보다 가볍게 취급)
* 스레드는 스레드 ID, 프로그램 카운터 (PC), 레지스터, 스택으로 구성되어 있다. 

<br><br>

### 2. **Mutlithreading**
* 다중 스레드 프로그래밍 장점
  * **응답성**
    * 스레드가 하나라면 화면 출력 + 사용자 입력 (하는 순간 화면 출력 잠깐 멈춤) + 스피커/마이크 (하는 순간 잠깐 멈춤) 
    * 멈추는 이유 : 프로세스는 run → block으로 갔다가 → ready 상태가 되기 때문. 
    * 일부 스레드가 처리 지연되더라도, 다른 스레드는 작업을 계속 처리할 수 있음. 
  * **자원 공유와 경제성**
    * 두 개의 작업을 각각 process에 저장하고 하나의 resource를 공유하게 되면 context switch가 발생하는데 이는 자주 발생하면 비효율적임. 
    * 두개의 process가 아니라 하나의 process 안에 두개의 thread로 사용하게 되면 cs가 발생하지 않기 때문에 효율적임. 
    * 즉 커널의 개입을 피할 수 있음.
  * **규모 적응성 (Scalability)**

<br>

* 다중 스레드 프로그래밍 모델
  * **다대일 모델**
    * 많은 사용자 수준 스레드와 하나의 커널 스레드.
    * 커널은 스레드의 존재를 모름
      * 라이브러리 수준에서 관리하기 때문에 더 효율적임. 
      * I/O가 필요해서 블록이 되면 커널 수준으로 넘어옴. 이럴 경우 커널은 하나의 스레드만 받기 때문에 사용자 수준의 스레드 하나가 block이 되면 나머지가 모두 block되는 단점.
  * **일대일 모델**
    * 사용자영역에서 만든 스레드만큼 커널에도 만드는 것.
    * 커널이 직접 관리
      * 커널이 각 스레드를 개별적으로 관리하기 떄문에 병행 수행이 가능함.  → block 되어도 나머지 스레드는 작업 수행 지속이 가능함. 
      * 커널이 많은 수의 스레드를 관리해야 하기 때문에 성능에 부담을 줄 수 있다.
  * **다대다 모델**
    * 혼합형 스레드로 n개 사용자수준 스레드 & m개의 커널 스레드 (n≥m)
    * 하나가 block이 되어도 병행 처리가 가능하다는 등 장점이 합쳐지게 됨. 