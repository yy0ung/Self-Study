# 안드로이드 Manifest
<br>

#### *manifest 파일은 안드로이드 빌드 툴, 안드로이드 OS, 구글 플레이 스토어에 앱에 관한 필수 정보를 제공한다.*

<br> 

### 1. **Manifest 목적**
#### *manifest 파일은 4가지를 선언하는데 그 목적이 있다.*

<br>

* **앱의 패키지 이름** : 고유한 앱 식별자로 사용됨.
* **앱의 구성 요소** : 4대 컴포넌트를 포함한 각 구성요소가 정의되어야 한다. 
  * 각 요소를 선언해줘야 시스템에서 이를 시작할 수 있다. 
    * `<activity>` : Activity
    * `<service>` : Service
    * `<receiver>` : BroadcastReceiver
    * `<provider>` : ContentProvider
  * 선언된 요소들은 intent 에 의해서 활성화 된다. 
* **권한 선언**
  * Android 앱은 민감한 사용자 데이터(예: 연락처, SMS) 또는 특정 시스템 기능(예: 카메라, 인터넷 액세스)에 액세스하기 위한 권한을 요청해야 한다. 이러한 권한들은 고유한 레이블로 식별된다.

~~~kotlin
<manifest ... >
    <uses-permission android:name="android.permission.SEND_SMS"/>
    ...
</manifest>
~~~

* **앱에 필요한 하드웨어, 소프트웨어 기능.**

<br><br>

### 2. **Manifest 규칙**
* manifest 파일에서 필수인 요소는 `<manifest>` ,`<application>` 이다.
* 그 하위 레벨에 속하는 `<activity>, <provider>` 등은 순서가 정해져있지 않다.

<br><br>

💡 \<application> 하위 속성

<br>

~~~kotlin
<application
        android:allowBackup="true"
        android:icon="@mipmap/ic_main"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_main_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.Surveasy"
        android:usesCleartextTraffic="true">
~~~

<br>

+ allBackup : 백업 및 복원 인프라에 참여하도록 허용하지 여부.
+ usesCleartextTraffic: 네트워크 트래픽을 사용하는지 여부. 모든 http url 에 대한 접근을 관리하는 태그.
+ supportsRtl : 어플리케이션이 오른쪽에서 왼쪽 레이아웃을 지원하는지 여부.  우리나라에서 해당 태그는 큰 의미 없음. 오른쪽에서 왼쪽으로 읽는 나라에서 지원된다.

<br><br><br>


##### 참고
##### https://developer.android.com/guide/topics/manifest/manifest-intro?hl=ko