# OS 운영체제 기본

<br>

### 1. **운영체제 다양한 정의**
* 컴퓨터 하드웨어를 관리하고 응용 프로그램 실행 환경을 제공하는 소프트웨어
* 운영체제도 프로그램. 항상 돌아가는 universal program 이다. 
* OS 는 위로는 process, app 들을 support 해주고, 아래로는 (HW) 관리 및 제어 하는 역할.

<br><br>

### 2. **운영체제 기능**
#### *한 마디로 "관리"하는 일이 주 업무.*

<br>

- 프로세스 관리 (동시 실행되는 프로세스 효율적으로 관리)
- 파일 관리 (파일 생성, 수정, 삭제, 조작, 백업)
- 네트워크 관리 (서비스 성능, 오류 분석, 품질관리 등)
- 메인 메모리 관리 (메모리 추적, 프로세스에 따른 메모리 할당)
- 보조 스토리지 관리 (스토리지 할당, 여유 공간 관리, 디스크 스케줄링)
- 입출력 장치 관리 (버퍼 캐싱 시스템 관리, 장치 드라이버 제공)
- 보안 관리 (시스템 보호 및 오류로 인한 시스템 손상 방지)
- 명령어 해석 시스템 (사용자와 시스템 간의 인터페이스, 인터프리터 등)

<br><br>

### 3. **용어 정리**
* **프로세서**
  * 하나 이상의 CPU 를 포함하는 물리적인 칩
  * 프로세서 내부 메모리인 "레지스터"는 컴퓨터에서 가장 빠른 메모리. 
* **메모리**
  * 저장장치.
  * 레지스터 - 캐시 - 메인메모리(RAM) - 보조기억장치 <br>
(속도 빠름, 용량 작음)      (속도 느림, 용량 큼)
* **프로세스**
  * 커널에 등록된 실행단위. 실행중인 프로그램에 해당함. 
  * 요청을 처리하고 프로그램을 수행하는 주체가 된다. 
  * 프로세스 여러 개가 하나의 resource를 사용하려하는 deadlock 상태를 관리함
* **비트**
  * 컴퓨터 저장장치의 기본 단위. 한 비트는 0과 1 두 값 중 하나를 가진다.
  * 1 byte = 8 bit 