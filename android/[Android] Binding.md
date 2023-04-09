# 안드로이드 Binding
<br>

### 1. **view binding**
* 각 XML 레이아웃 파일의 binding 클래스를 생성한다. binding 클래스의 instance에는 상응하는 레이아웃에 id가 있는 모든 view의 직접 참조가 포함된다.
* findViewById 와 다른점
  * Null 안전 : View의 직접 참조를 생성하기 때문에 유효하지 않은 view id로 인해 null pointer exception이 발생할 위험이 없다. 
  * 유형 안전 : 각 binding class의 필드 유형이 XML 파일에서 참조하는 view와 일치해서 클래스 변환 예외 발생 위험이 없다.
* 사용방법
  * viewBinding 을 사용하려면 build.gradle 파일에 viewBinding 요소를 추가한다.
  * activity
    * inflate( ) 함수를 이용해 instance를 생성한다. 
    * root view 를 setContentView에 전달하여 활성 뷰를 만든다.

<br>

~~~kotlin
private lateinit var binding: ResultProfileBinding

    override fun onCreate(savedInstanceState: Bundle) {
        super.onCreate(savedInstanceState)
        binding = ResultProfileBinding.inflate(layoutInflater)
        val view = binding.root
        setContentView(view)
    }
~~~

  * fragment
    * activity에서와 동일하게 onCreateView 안에 binding에 필요한 코드를 작성한다.
    * fragment는 activity 보다 오래 지속되기 때문에 onDestroyView( ) 매서드에서 참조 정리를 해줘야 한다.

<br>

~~~kotlin
override fun onDestroyView() {
        super.onDestroyView()
        _binding = null
    }
~~~

<br><br>

### 2. **data binding**
* 데이터 결합 라이브러리는 프로그래매틱 방식이 아니라 선언적 형식으로 레이아웃의 UI 구성요소를 앱의 데이터 소스와 결합할 수 있는 라이브러리.
* layout 태그를 통해 XML 파일에서 View에 텍스트 등을 할당할 수 있음.

<br>

~~~kotlin
<layout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:app="http://schemas.android.com/apk/res-auto">
        <data>
            <variable
                name="viewmodel"
                type="com.myapp.data.ViewModel" />
        </data>
        <ConstraintLayout... /> <!-- UI layout's root element -->
    </layout>
~~~

<br>

* 코드 가독성이 좋아지고 간결 해진다는 장점이 있지만 클래스 파일이 늘어나고 빌드 속도가 느려진다는 단점도 있다. MVVM 패턴 등과 함께 사용하면 효율이 올라간다. 
* 사용하는 activity에서 data class를 초기화해주고, XML 파일에서 아래와 같은 형식으로 바인딩 해줄 수 있다. 

<br>

~~~kotlin
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        val binding: ActivityMainBinding = DataBindingUtil.setContentView(
                this, R.layout.activity_main)

        binding.user = User("Test", "User")
    }
~~~

<br>

~~~kotlin
<TextView android:layout_width="wrap_content"
              android:layout_height="wrap_content"
              android:text="@{user.firstName}" />
~~~
