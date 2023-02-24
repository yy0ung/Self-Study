# 안드로이드 Activity & Service 심화

<br>

### 1. **Activity - bundle**
* 여러 타입의 값을 저장하는 Map class. 
* 데이터 저장 객체로 상태 저장 및 복구에 사용된다. 
  * onStop( ) 전에 onSavedInstanceState에서 데이터를 저장, onStart( ) 이후에 onRestoreInstanceState 에서 복구.
* Intent 의 extra 이용하여 다른 구성요소에 데이터 전달. 이때 입력되는 것이 Bundle 객체이다. 

<br><br>

### 2. **Activity - Parelable**
* 직렬화하는 방법. 객체를 묶어주고 풀어주기 위한 Interface. 
* activity 간 데이터를 공유해야 하는 경우 intent 를 하나 생성하고 putExtra( ) 로 데이터를 넣어 데이터를 공유하는데, 이때 primitive type 은 바로 넣어주면 되지만 객체의 경우는 직렬화된 상태로 전달해야 한다. 

<br>

💡 Serializable 은 자바의 표준 인터페이스로 직렬화를 가능하게 한다. 간단하게 구현 가능하지만 내부적으로 가비지 콜렉션이 발생하여 성능이 떨어진다. 
<br> 반면 Parcelable 은 안드로이드 SDK 포함 인터페이스로 불필요한 객체를 덜 생성하여 성능이 더 높다.

<br><br>

### 3. **Service - service 종류**
#### *서비스는 어플이 UI 없이 백그라운드에서 특정 시간 동안 실행되는 것.*

<br>

* **포그라운드**
  * 상태바에 알림이 제공되어야 한다. 실제로 어떤 작업이 실행 중인지 눈으로 보여야 함.
  * 입력한 명령이 실행되어 결과가 출력될 때까지 기다려야 함.
  * 음악 어플에서 음악이 실행 중일 때 상태바에서 일시정지, 넘기기 등이 가능해야 하는 것. 다운로드 받을 때 알림창에 “다운로드 중” 등의 알림이 뜨면서 다운로드가 계속 되는 것. 

<br>

* **백그라운드**
  * 사용자에게 보이지 않는 작업이 수행됨. 
  * 특정 파일을 업로드하는 동안 해당 어플을 끄고 다른 일을 해도 업로드 멈추지 않는다. (알림창과 상관 x), 
  * 어플을 업데이트하는 중 스토어 어플을 종료해도 업데이트 멈추지 않음.

<br>

* **바인드**
  * 포그라운드, 백그라운드 서비스는 앱 내에서 시작된 서비스가 끝나기 전까지 계속 실행되지만 바인드 서비스는 어플과 통신하다가 서비스를 부른 액티비티가 종료되면 작업이 끝나지 않아도 종료된다. 

<br><br><br>

##### 참고
##### https://developer.android.com/guide/components/activities/parcelables-and-bundles?hl=ko
##### https://developer.android.com/guide/components/services?hl=ko