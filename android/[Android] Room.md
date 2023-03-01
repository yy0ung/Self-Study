# 안드로이드 Room
#### *SQLite를 완벽히 활용하면서 원활한 데이터베이스 액세스가 가능하도록 SQLite의 추상화 계층을 제공하기 때문에 SQLite API 직접 사용하는 것 보다 Room 사용이 권장됨.*
<br><br>

### **Room 구성요소**

<br>

### **1. 데이터베이스 클래스**
#### *기본 엑세스 포인트 역할* 

<br>

* 데이터베이스를 보유할 클래스를 정의한다. 
* 연결된 데이터 항목을 모두 나열하는 entities 배열이 포함된 @Database 주석이 달려야 함.
* 클래스는 RoomDatabase 를 확장하는 추상 클래스여야 함.

<br>

~~~kotlin
@Database(entities = [User::class], version = 1)
abstract class AppDatabase : RoomDatabase() {
    abstract fun userDao(): UserDao
}
~~~

<br><br>

### **2. 데이터베이스 항목**
* 앱 db의 테이블을 나타냄.
* 데이터 항목을 정의함. 

<br>

~~~kotlin
@Entity
data class User(
    @PrimaryKey val uid: Int,
    @ColumnInfo(name = "first_name") val firstName: String?,
    @ColumnInfo(name = "last_name") val lastName: String?
)
~~~

<br><br>

### **3. 데이터베이스 엑세스 객체 (DAO)**
* 앱이 데이터베이스의 데이터를 쿼리, 업데이트, 삽입, 삭제하는데 사용할 수 있는 메서드를 제공. 

<br>

~~~kotlin
@Entity
data class User(
    @PrimaryKey val uid: Int,
    @ColumnInfo(name = "first_name") val firstName: String?,
    @ColumnInfo(name = "last_name") val lastName: String?
)
~~~

<br><br>

💡 room db 를 사용할 경우에는 인스턴스를 만들어서 사용할 수 있다. 

<br>

```kotlin
val db = Room.databaseBuilder(
            applicationContext,
            AppDatabase::class.java, "database-name"
        ).build()
```