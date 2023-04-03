# 안드로이드 BackStack
<br>

### **onBackPressed()**
* 뒤로가기 버튼을 눌렀을 때 처리하는 함수. 
* 두번 눌러 종료하기 등을 구현하기 위해 이 함수를 변형해 사용한다.

<br><br>

### **Fragment BackStack**
* fragment 를 add 하고 난 상태에서 뒤로가기 버튼을 누르게 되면 activity 의 onBackPressed() 가 실행되며 어플이 종료된다. 
* A fragment 에서 B fragment 로 이동하고 난 후에 뒤로가기 버튼을 누를 경우 A 로 이동하고 싶다면 fragment backstack 을 사용해야 한다 
* 아래 코드는 stack 에 쌓인 fragment 을 하나씩 없애주고, stack 에 fragment 가 남아있을 경우 그 fragment 를 보여주게 하는 코드이다.

<br>

~~~kotlin
val transaction = supportFragmentManager.beginTransaction()

// 해당 transaction 을 backstack 에 저장.
transaction.addToBackStack(null)

// transaction 실행
transaction.commit()
~~~