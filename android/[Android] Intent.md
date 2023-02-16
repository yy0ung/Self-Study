# 안드로이드 Intent
<br>

#### *Intent 는 메시징 객체로, 다른 앱 구성요소로 부터 작업을 요청하는데 사용.*

<br> 

### 1. **Intent 유형**
* **명시적 인텐트**
  * 인텐트를 충족하는 것이 무엇인지 직접 지정함. 앱 안에서 다음 구성요소를 지정할 때 사용하며 구성요소가 어떤 인텐트 필터를 선언하든 무관하다.
  * 생성자가 앱에 context 를 제공하고 구성요소에 앱 내의 class 객체를 완전하게 제공한다. 
  
  <br>

~~~kotlin
// Executed in an Activity, so 'this' is the Context
// The fileUrl is a string URL, such as "http://www.example.com/image.png"

val downloadIntent = Intent(this, DownloadService::class.java).apply {
    data = Uri.parse(fileUrl)
}
startService(downloadIntent)
~~~  
  

<br><br>

* **암시적 인텐트**
  * 특정 구성요소의 이름을 정확하게 명시하지는 않지만 수행할 작업을 선언하여 다른 구성요소가 이를 처리할 수 있도록 한다.
  * 암시적 인텐트는 startActivity( ) 로 전송한 인텐트를 처리할 앱이 전혀 없을 수 있기 때문에 null 체크를 하고 사용하는 것이 안전.

<br>

~~~kotlin
// Create the text message with a string
val sendIntent = Intent().apply {
    action = Intent.ACTION_SEND
    putExtra(Intent.EXTRA_TEXT, textMessage)
    type = "text/plain"
}

// Verify that the intent will resolve to an activity
if (sendIntent.resolveActivity(packageManager) != null) {
    startActivity(sendIntent)
}
~~~

<br>

> 💡 암시적 인텐트를 사용하면 Android 시스템에서 시작할 적절한 구성 요소를 찾음. 이때 인텐트의 내용을 기기에 있는 다른 여러 앱의 매니페스트 파일에서 선언된 인텐트 필터와 비교하는 방법을 사용.해당 인텐트와 일치하는 인텐트 필터가 있으면 시스템에서 해당 구성 요소를 시작하고 이를 Intent객체를 전달. 호환되는 인텐트 필터가 여러 개인 경우, 시스템에서 대화상자를 표시하여 사용자가 어느 앱을 사용할지 직접 선택할 수 있게 함.

<br><br>

### 2. **Intent Filter**
* 앱의 manifest 파일에 들어있는 표현으로, 해당 구성요소가 수신하고자 하는 인텐트의 유형을 나타낸다. 암시적 인텐트를 수신하기 위해 선언해야 하는 요소이다. 선언하지 않은 경우 명시적 인텐트로만 시작이 가능하다.
* 즉 인텐트 필터는 인텐트를 필터링해서 자신이 현재 필요한 인텐트를 받기 위해 사용하는 것. 가장 적절한 컴포넌트를 받기 위해서 사용하는 것이다.
* ex) 어플을 키자마자 실행될 activity 를 암시적 인텐트를 이용해 선언 가능하다.
* 하위 요소
  * \<action\> : name 특성에서 허용된 인텐트 작업을 선언.
  * \<data> : 허용된 데이터 유형을 선언.
  * \<category> : name 특성에서 허용된 인텐트 카테고리 선언.

<br>

> 💡 암시적 인텐트를 수신하려면 CATEGORY_DEFAULT
 카테고리를 인텐트 필터에 포함해야 한다.
 startActivity()및 startActivityForResult()
 메서드는 마치 CATEGORY_DEFAULT범주를 선언한 것처럼 모든 인텐트를 취급한다. 이 카테고리를 인텐트 필터에서 선언하지 않으면 액티비티에 어떤 암시적 인텐트도 확인되지 않는다.

<br><br><br>

🔑 예시 코드

~~~kotlin
<activity android:name="MainActivity">
    <!-- This activity is the main entry, should appear in app launcher -->
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>

<activity android:name="ShareActivity">
    <!-- This activity handles "SEND" actions with text data -->
    <intent-filter>
        <action android:name="android.intent.action.SEND"/>
        <category android:name="android.intent.category.DEFAULT"/>
        <data android:mimeType="text/plain"/>
    </intent-filter>
    <!-- This activity also handles "SEND" and "SEND_MULTIPLE" with media data -->
    <intent-filter>
        <action android:name="android.intent.action.SEND"/>
        <action android:name="android.intent.action.SEND_MULTIPLE"/>
        <category android:name="android.intent.category.DEFAULT"/>
        <data android:mimeType="application/vnd.google.panorama360+jpg"/>
        <data android:mimeType="image/*"/>
        <data android:mimeType="video/*"/>
    </intent-filter>
</activity>
~~~