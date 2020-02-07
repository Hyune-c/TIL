# Mutable, Immutable  

인스턴스 생성 후 Mutable 객체는 인스턴스의 내용이 변할 수 있지만, Immutable 객체는 변할 수 없습니다.

| Feature        | Mutable                       | Immutable                                           |
| -------------- | ----------------------------- | --------------------------------------------------- |
| 멤버 변수 변경 | Y                             | N                                                   |
| Getter         | Y                             | Y                                                   |
| Setter         | Y                             | N                                                   |
| Example        | java.util.Date, StringBuilder | Boxed primitive objects(Integer, String)<br />Lamda |


## Why is String immutable? 
Security
- parameters are typically represented as String in network connections
, database connection urls, usernames/passwords etc. If it were mutable, these parameters could be easily changed.

Synchronization and concurrency
- making String immutable automatically makes them thread safe thereby solving the synchronization issues.

Caching
- when compiler optimizes your String objects, it sees that if two objects have same value (a="test", and b="test") 
and thus you need only one string object (for both a and b, these two will point to the same object).

Class loading
- String is used as arguments for class loading. 
If mutable, it could result in wrong class being loaded (because mutable objects change their state).


## Why don't use Immutable
- Immutable 한 객체 간의 연산은 새로운 Immutable 객체를 생성해서 Heap 영역을 차지하게 됩니다. 
- 물론 Garbage Collection 이 이를 정리하지만, GC 의 동작은 Java 의 속도를 저하시키는 가장 큰 요인 중 하나입니다.


## String vs StringBuilder vs StringBuffer

| Feature       | String            | StringBuilder    | StringBuffer     |
| ------------- | ----------------- | ---------------- | ---------------- |
| 불변성        | Immutable         | Mutable          | Mutable          |
| append String | Create new Object | append in memory | append in memory |
| 동시성        | Y                 | N                | Y                |

## 참고자료 
- https://novemberde.github.io/2017/04/15/String_0.html