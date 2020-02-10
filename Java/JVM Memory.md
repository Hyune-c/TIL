# JVM Memory

![JVM Runtime Data Area](https://user-images.githubusercontent.com/55722186/74124316-29f27080-4c15-11ea-9c62-5af7769c2c73.png)

### Method Area
- 모든 스레드가 공유하는 영역입니다.
- 정적 필드, 상수, 메소드, 생성자 코드가 있습니다.

### Heap Area 
- 스택 영역의 필드에서 참조가 가능합니다.
- 참조하는 필드나 변수가 없다면 GC 가 자동으로 제거합니다.
- 배열, 객체가 있습니다.

### Stack Area
- JVM 은 메소드를 호출할 때마다 프레임을 추가하고, 종료되면 제거합니다.
- 프레임 내부에는 로컬 변수 스택이 있는데, 기본 타입 변수와 참조 타입 변수가 추가되거나 제거됩니다.
    - 참조 타입의 변수는 Heap Area 의 주소가 저장됩니다.


### 참고 자료
https://programmer-seva.tistory.com/72