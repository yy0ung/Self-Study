# 안드로이드 REST API & Retrofit

<br>

### 1. **REST API**
#### *Representational State Transfer API*

<br>

* **rest** 
  * 자원 (resource, URI), 행위 (Verb, http method), 표현 (representations)
  * rest는 네트워크 아키텍쳐 원리의 모음. 자원을 정의하고 자원에 대한 주소를 지정하는 방법 전반을 말한다.
  * uri를 통해 자원을 명시하고, method를 통해 자원에 대한 CRUD operation을 적용하는 것을 의미한다.

<br>

* rest 특징
  * **유니폼 인터페이스** : 한정적이고 통일된 인터페이스 아키텍쳐 스타일
  * **무상태성** : 작업을 위한 상태정보를 저장, 관리하지 않기 때문에 요청만 단순히 처리함. 의존하지 않고 자유도가 높다.
  * **캐시 가능** : 웹 표준을 그대로 사용하기 때문에 웹에서 사용하는 기존 인프라를 그대로 활용할 수 있다. 
  * **자체 표현 구조**: rest api만 보고 쉽게 이해가 가능한 구조로 이루어져 있다. 
  * **client - server 구조** : 클라이언트와 서버에서 개발해야 할 내용이 명확히 나눠져 있기 때문에 서로간 의존성이 줄어든다.
  * **계층형 구조** : 구조상의 유연성을 둘 수 있고 중간 매체를 사용할 수 있다.

<br>

### 2. **Retrofit**
#### *http 통신을 편리하게 만들어주는 라이브러리. okhttp의 상위 구현체로 속도, 편의성, 가독성 측면에서 장점을 가진다.*

<br>

>okhttp : java 라이브러리이며 이는 retrofit의 베이스가 된다. 

<br>

* 구성요소
  * **DTO** - Data Transfer Object 모델로 받은 데이터를 가공하고 타입 변환하는데 사용.
  * **Interface** - 사용할 동작 (http method)를 정의해둔 인터페이스
  * **Retrofit.Builder 클래스** - 인터페이스를 실제로 사용할 인스턴스. baseUrl / Converter 설정

<br>

* Retrofit 객체
  * Retrofit.Builder 를 통해서 객체를 초기화하고 설정이 가능하다.
  * “baseUrl” 에는 통신할 base url 을 넣어준다.
  * “client” OkHttp 객체를 이용해서 통신 로그를 찍을 수 있게 한다. setLevel을 통해서 어느 단계까지 로그를 볼 것 인지 설정할 수 있다.
  * “addConverterFactory” 에는 Json을 Gson형태로 변환시킬 수 있는 라이브러리인 GsonConverterFactory를 사용할 수 있다.
    
    <aside>
    💡 Gson : java 에서 Json 을 파싱하고 생성하기 위해 사용되는 오픈소스. Java Object 와 Json문자열 간의 변환을 지원.
    
    </aside>

<br>

~~~kotlin
  //retrofit client 선언
object RetrofitClient {
    private var retrofitClient : Retrofit? = null

    fun getClient(baseUrl : String) : Retrofit?{
        Log.d(TAG, "getClient: called")

        val client = OkHttpClient.Builder()
        val loggingInterceptor = HttpLoggingInterceptor(object :HttpLoggingInterceptor.Logger{
            override fun log(message: String) {
                Log.d(TAG, "log: message ${message.toString()}")
            }
        })
        loggingInterceptor.setLevel(HttpLoggingInterceptor.Level.BODY)
        client.addInterceptor(loggingInterceptor)

        if(retrofitClient == null){
            retrofitClient = Retrofit.Builder()
                .baseUrl(baseUrl)
                .client(client.build())

                .addConverterFactory(GsonConverterFactory.create())
                .build()
        }
        return retrofitClient
    }
}
~~~

<br>



<br>

* Retorfit 응답처리
  * 서버로부터 응답을 받아서 처리할 때는 call 혹은 response 를 통해 처리한다.
  * call 을 통해서 처리하면 `onResponse`, `onFailure` 를 이용하여 명시적으로 성공, 실패로 나누어 처리하게 된다.
  * response 를 이용하면 성공 실패로 나누어 데이터를 처리하는 것이 아니라 서버로 부터 code를 받아서 프론트에서 분기해 데이터를 처리할 수 있다.