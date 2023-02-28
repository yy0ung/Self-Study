# 안드로이드 ViewModel
#### *AAC ViewModel & MVVM 패턴에서의 ViewModel*
<br><br>

### **AAC viewModel** 
* 안드로이드 아키텍쳐 컴포넌트 (AAC) 에서 제공하는 추상 클래스
* 뷰에 사용되는 데이터를 유지시키면서 라이프사이클을 알고 있는 클래스.

<br>

### **MVVM 패턴에서의 ViewModel**
* 뷰와 모델 사이의 데이터를 관리하고 바인딩하는 요소.

<br>

> 둘은 이름만 같고 실제로 아무런 관련이 없다.

<br>

💡 ACC viewModel 은 대표적인 사용 예시로 *“화면이 회전되어도 데이터를 보존해준다”* 를 자주 찾아볼 수 있듯이 데이터를 유지시키는 것이 주요한 기능이다. MVVM 패턴에서 말하는 viewModel 과는 그 정의가 다른 것을 알 수 있다. 

<br>

💡 MVVM 패턴 안의 viewModel 아키텍쳐를 AAC viewModel 을 사용해서 구현하는 경우가 많고 둘의 이름이 같기 때문에 혼돈되는 부분이 있는 것이다. 뷰와 모델 사이에서 데이터를 관리하고 바인딩해주는 역할을 해야하는 MVVM 패턴 안의 viewModel 을 AAC viewModel 을 이용해서 구현한다면 AAC viewModel 이 가지고 있는 기능도 함께 사용할 수 있기 때문에 많은 사람들이 그렇게 사용할 뿐이다. <br> *당연히 MVVM 패턴을 구현할 때 AAC viewModel을 사용하지 않아도 된다.*