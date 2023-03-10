# OS CPU Scheduling overview
<br>

### 1. **Scheduling 기본 개념**
* 하나의 프로세스 작업이 끝나면 다음 작업을 수행해야 하는데 다음 작업으로 어떤 프로세스를 선택할지 결정하는 알고리즘을 말함. 
* CPU는 하나인데 동시에 프로세스가 여러개 실행되어야 하기 때문에 CPU 할당 순서 및 방법을 결정하기 위함. → 어떤 프로세스를 running 상태로 보낼지 정하는 것이 스케줄링.
* CPU 를 효율적으로 사용해 시스템 성능을 향상시키기 위한 것으로 목적에 맞는 지표를 고려하여 정책을 선택하면 됨.
* 어떤 프로세스를 다음에 실행할지 고르는 작업을 하는 것이 "Scheduler" (스케줄러) 이다.

<br><br>

### 2. **Scheduling 정책**
* **선점** (Preemptive, 누가 내 것을 빼앗을 수 있다)
  * 자원을 빼앗길 수 있음
  * 응답성이 높아지지만 context switch overhead가 많이 발생함. 

<br>

* **비선점** (Non-preemptive)
  * 할당 자원을 스스로 반납할 때까지 사용 (I/O가 발생하거나 종료될 때까지 안바뀜)
  * Context switch overhead가 적지만 우선순위가 높은 것을 처리하기 어려움

<br><br>

### 3. **Dispatcher**
* CPU 스케줄러가 선택한 프로세를 CPU 에 올려주는 역할을 함.
* context switch 시에 호출되기 때문에 빠르게 수행될 수록 성능이 좋다.
* Dispatcher 와 Scheduler 가 하는 일을 합쳐서 Scheduling 이라고 부른다.