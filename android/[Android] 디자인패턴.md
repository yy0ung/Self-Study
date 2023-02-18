# 안드로이드 디자인패턴 ( MVP, MVVM )
<br>

### 1. **MVP**
#### *Model + View + Presenter*
#### *UI (View) 와 비지니스 로직 (Model) 을 분리하고 서로 간의 상호작용에 Presenter를 사용하면서 둘의 의존성을 최소화 하는 것.*

<br>

* **Model**
  * 프로그램 내부적으로 쓰이는 데이터 저장 및 처리
  * 다른 두 요소에 의존적이지 않음. 
* **View**
  * UIViewController 를 가짐. 
  * input을 받고 결과를 보여주는 역할을 한다.
  * Model에서 처리된 데이터를 Presenter를 통해 받아서 유저에게 보여줌. 
  * Presenter에 매우 의존적.
* **Presenter**
  * view에서 input 이 들어오면 받아서 처리하고 다시 view로 보내는 플로우를 가짐. data만 전달하며, 결과를 보여주는 방식은 view 혼자 담당함.
  * 화면에 보여줄 것들을 관리하는데 화면 그 자체는 아님. 그래서 view와 presenter는 1:1 관계.
  * 인터페이스를 통해 상호작용함. 

<br>

#### *문제 : view 하나를 만들 때마다 presenter를 모두 하나씩 만들어줘야함. 로직이 아주 비슷한데 두개씩 만들어서 관리하는 것이 비효율적.*

<br><br>

### 2. **MVVM**
#### *Model + View + ViewModel*
#### *view와 model이 분리되어 있고 분리된 로직 사이에서 뷰의 이벤트에 따라 모델이 데이터를 반환하거나 저장하도록 하는 뷰모델이 존재.*

<br>

* **Model**
  * DB 사용이나 retrofit을 이용한 backend api 호출이 보편적. 
* **View**
  * 사용자의 액션을 받음. ( action -> input )
  * viewModel의 데이터를 관찰해서 (live data, observe) UI 를 갱신. 데이터의 변화를 알아차리고 자동으로 화면을 갱신할 수 있다.
* **ViewModel**
  * view한테 화살표 없음. 그리는 데는 관여하지 않고  데이터만 바꾸면 그걸 view가 보고 확인. 
  * view가 요청한 데이터를 model로 요청하고 model 로부터 요청한 데이터를 받음.