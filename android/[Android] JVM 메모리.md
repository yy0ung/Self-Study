# JVM 메모리

<br>


- JVM ( Java Virtual Machine )
- 자바 소스코드를 컴파일해서 나온 자바 바이트 코드를 실행하는 주체.
- `Class Loader`, `Execution Engine`, `Garbage Collector`, `Runtime Data Area`

<br>

### 1. `Class Loader`

- `.java` 파일을 컴파일하면 `.class` 파일이 생성됨.
- JVM 내로 class 파일을 로드하고, `Runtime Data Area` 로 적재하는 역할을 함.

<br><br>

### 2. `Execution Engine`

- 메모리에 적재된 바이트코드를 명령어 단위로 실행하는 역할을 함.

<br><br>

### 3. `Garbage Collector`

- 힙 메모리 영역에 생성된 객체 중 참조되지 않은 객체를 탐색해서 제거.
- 만약 기존에 String 타입으로 선언된 값 뒤에 String 을 더 붙이게 되면 변수명은 그대로이지만 값이 변하게 됨. → `String name = "a"` // `name+="b"`
    - 이 경우 기존 스택의 “name” 은 “a” 에서 “ab” 을 가리키도록 변하게 되며, 기존의 “a” 데이터는 스택과의 연결이 끊어짐.
    - 이를 제거해 주는 것이 GC 의 역할.

<br><br>

### 4. `Runtime Data Area`

- `Method area`
    - 모든 스레드가 공유하는 영역.
    - 클래스, 인터페이스, 메소드, 정적변수 등 바이트코드를 보관.

<br>

- `Heap area`
    - 모든 스레드가 공유하는 영역.
    - 메소드 영역에 로드된 클래스만 생성이 가능하고, GC 가 참조되지 않는 메모리를 확인하고 제거함.
    - 모든 Object 타입( Integer, String, ArrayList )은 heap 영역에 생성. ( new 키워드로 생성된 객체와 배열이 생성되는 곳 )
    - 힙 영역에 있는 오브젝트들을 가리키는 레퍼런스 변수가 스택에 저장됨.
        - `Heap p = new Heap()`
            - `p` 는 스택에 생성 → 힙 영역의 주소값을 가지고 있음. (참조)
            - `Heap` 의 인스턴스는 힙에 생성

<br>

- `Stack area`
    - 힙 영역에 생성된 Object 타입 데이터의 참조값이 할당됨.
    - 메소드를 호출할 때마다 개별적으로 스택이 생성됨.
    - 중괄호가 닫히면서 함수가 종료되면 호출 함수의 범위에서 스택에 할당된 값들이 모두 해제됨.

<br>

- `PC Register`
    - 스레드가 시작될 때 생성되며, 스레드마다 하나씩 존재.
    - 현재 수행 중인 JVM 명령의 주소를 가짐. → 스레드를 돌아가면서 수행 가능함.

<br>

- `Native method stack`
    - 자바 외 언어로 작성된 코드를 위한 메모리영역.