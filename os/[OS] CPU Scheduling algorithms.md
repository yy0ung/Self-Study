# OS CPU Scheduling Algorithms
#### *CPU scheduling 은 ready queue 에 있는 어떤 프로세스에 CPU 코어를 할당할 것인지를 결정하는 문제를 다룬다.*
<br>

### 1. **First Come, First Served (FCFS)**
* 가장 간단한 알고리즘으로 선입 선처리 알고리즘이다. 
* 스케줄링 기준은 도착시간, 자원을 효율적으로 사용할 수 있음 (overhead low) 
* Batch system (일괄처리 시스템) 에 적합. interactive system에 부적합. 
* 순서대로 들어와서 할 일을 하고 순서대로 나가게 됨.
* 비선점 알고리즘으로, 한 프로세스가 지나치게 오래 CPU 를 점유할 수 있어 손해가 클 수 있다.

<br><br>

### 2. **Shortest Job First**
* 최단 작업 우선 알고리즘.
* 가장 작은 프로세스를 먼저 처리. ex) 소량 계산대
* 평균 대기시간, 시스템 내 프로세스 수 최소화 (시간 짧은거 바로 빼기 때문)
  * 시스템 효율 향상
* 무한대기 (starvation) 현상 발생. 긴 프로세스는 자원을 할당받지 못할 수 있음.

<br><br>

### 3. **Shortest Remaining Time Next**
- Preemptive 스케줄링 : 잔여 실행시간이 더 적은 프로세스가 ready 상태가 되면 선점됨.
- 잔여 실행을 계속 추적해야 해서 overhead
- 구현 및 사용이 비현실적

<br><br>

### 4. **Round-Robin**
- 원형으로 돌면서 하는 스케줄링.
    - 선입 선처리 스케줄링과 유사하지만 선점이 추가된 알고리즘.
    - Ready Q에 다시 들어갈 때 맨 뒤에 다시 들어감.
- 도착시간 기준이지만 자원 사용에 제한 시간이 있음.
- 독점을 방지할 수 있지만 processor가 계속 바뀌어야 하기 때문에 context switch, overhead가 크다는 단점을 가지고 있음.
- Time quantum (시간 할당량) 이 시스템 성능을 결정하는 핵심 요소.