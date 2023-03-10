# OS Process overview & PCB
##### *2023-03-07 process 생성 업데이트*
<br>

### 1. **Process Concept**
* 커널에 등록되고 관리 하에 있는 작업. 각종 자원들을 요청하고 할당 받을 수 있는 개체.
* 쉽게 말해, 현재 실행 중인 프로그램을 말한다. 
  * 프로그램 그 자체가 프로세스는 아니다. 프로그램 실행파일이 메모리에 적재될 때 프로그램은 프로세스가 된다.
* 프로세스 메모리 배치
  * text (code) : 실행 코드 (크기 고정)
  * data : 전역 변수 (크기 고정)
  * heap : 프로그램 실행 중에 동적으로 할당되는 메모리
  * stack : 함수를 호출할 때 임시 데이터 저장소

<br><br>

### 2. **Process state**
#### *프로세스는 실행되면서 그 상태가 변함. 그 프로세스의 현재 활동에 따라서 정의됨.*

<br>

* 프로세스 상태
  * *NEW*
    * 프로세스가 생성 중 (PCB 함께 생성). 아직 OS 의 승인은 x
    * 가용메모리 공간 체크
      * 메모리 할당을 받을 수 있으면 *READY*
      * 메모리 할당이 불가한 상태면 *SUSPENDED READY*

<br>

  * *READY* 
    * 프로세서가 할당되기를 기다린다. (프로세서 제외 모든 자원이 할당된 상태)
    * Dispatch (schedule)
      * *READY -> RUNNING*

<br>

  * *RUNNING* 
    * 명령어가 실행되는 중
    * Preemption
      * 현재 running 상태의 프로세스보다 ready Queue에 대기하고 있는 프로세스의 우선순위가 더 높으면 위치가 바뀌게 됨.
      * *RUNNING -> READY*
    * Block/Sleep
      * 자발적으로 자러 간 상태 (휴식) 
      * 자기 의지로 대기열에서 이탈했다가 다시 대기열의 마지막으로 들어가게 됨. (sleep(ms) 가 call 된다면 대기열 앞에 있는 스레드들 다 수행되고 난 이후에 수행되기 떄문에 수행되기까지 걸리는 시간은 ms+alpha 의 시간이 된다. 
      * *RUNNING -> ASLEEP*

<br>

  * *BLOCK/ASLEEP*
    * 프로세서 외 다른 자원을 기다리는 상태
    * wake-up
      * *ASLEEP -> READY*

<br>

  * *SUSPENDED*
    * 외부요인에 의해서 의도하지 않게 메모리를 뺴앗긴 상태
    * 커널 혹은 사용자에 의해 발생.

<br>

  * *TERMINATE* 
    * 프로세스의 실행이 종료된다. 

<br><br>

### 3. **Process Control Block (PCB)**
* OS가 프로세스 관리에 필요한 정보를 저장.
    * 프로세스를 (다시) 시작시키는데 필요한 정보를 모두 저장하는 저장소 역할을 한다.
* 각 프로세스들에 대한 상세정보를 저장. (Kernel이 가지고 있어야 함.)
* PCB 참조 및 갱신 속도는 OS의 성능을 결정짓는 중요한 요소 중 하나이다.


<br><br>

### 4. **Process 생성**
* process 는 PID 라는 고유한 아이디를 가지고 있다.
* 생성 과정
  * 생성 → 메모리에 복사 → text 영역에 올리고 PCB 를 붙인다. (이때 VMS 가상메모리공간은 확보)
* (UNIX 체제 내의 생성)
  * fork() : 이러한 생성과정이 복잡하니까 일단 복사를 해서 다른 process을 생성하고 내부의 코드만 바꿔서 사용한다. PID 가 완전히 다른 새로운 프로세스가 생기는 것이다. 
  * exec() : 새로운 프로세스가 생기는 것이 아니라 기존의 PID 는 유지되고 그 프로세스에 덮어쓰기가 되는 것.
