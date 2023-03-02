# 안드로이드 Context

<br>

### 1. **Context 란?**
* 어플리케이션의 현재 상태를 가지고 있음.
* 시스템이 관리하는 activity, app의 정보를 얻기 위해 사용.
* context의 잘못된 사용은 메모리 릭 문제로 이어질 수 있음.

<br><br>

### 2. **Context 종류**
* **Application Context**
  * Activity 에서 applicationContext 프로퍼티를 통해 얻을 수 있는 싱글톤 인스턴스. 
  * app의 라이프사이클과 묶여있어 현재 context나 activity를 벗어나서도 context가 필요한 작업에서 사용 가능함.
    * ex) app 전역에서 사용할 라이브러리를 Main에서 초기화 하는 경우
  * 하지만 이 context는 Activity context가 지원하는 모든 것을 지원하지는 않음. GUI 관련 동작에 있어 오류가 발생하기도 함.
  * activity 와는 달리 GC 가 일어나지 않기 때문에 메모리를 직접 해제하지 않으면 메모리 릭이 발생할 수 있다.

<br>

* **Activity Context**
  * activity 안에서만 사용이 가능. 특정 Activity의 라이프 사이클과 종속되어 있음. 
  * Activity가 소멸되면 해당 context도 함께 소멸.
  * 가장 가까운, 밀접한 스코프의 context를 골라 사용하되, 전역에서 사용된다면 Application Context 사용하면 됨.


<br><br><br>


##### 참고
##### https://velog.io/@haero_kim/Android-Context-%EB%84%88-%EB%8C%80%EC%B2%B4-%EB%AD%90%EC%95%BC