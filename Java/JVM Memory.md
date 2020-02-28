# JVM Memory

![](../image/Java/JVM%20Memory_JVM1.png)

![JVM Runtime Data Area](https://user-images.githubusercontent.com/55722186/74124316-29f27080-4c15-11ea-9c62-5af7769c2c73.png)

## Memory Area

### Method
- 모든 스레드가 공유하는 영역
- ClassLoader 가 필요한 시기에 필요한 요소를 호출합니다.	
- 구성 요소 : Class(construcor 등), Constant Pool, static field, final class

### Heap
- 스택 영역에서 참조가 가능합니다.
- 사용되지 않는 대상은 GC 가 자동으로 제거합니다.
- 메모리의 끝 주소부터 저장됩니다.	
- 구성 요소 : Array, 할당된 Object	

### Stack
- 메소드가 추가될 때마다 Frame 이 추가됩니다.
- args 가 가장 아래에 저장됩니다.
- 메모리의 시작 주소부터 저장됩니다.	
- 구성 요소 : Frame(local/ reference field 등)	

### PC Register
- per thread 자료구조
- 구성 요소 : PC와 명령을 저장합니다.

## 확인 중 ..
- 프로그램 실행 시점에 클래스로더가 .class 파일을 읽어 Method 영역에 해당하는 것들을 모두 올려놔야된다고 생각했습니다.  
왜냐하면 필요할 때 올린다는건 프로그램 실행 중에 static/Class 등을 .class 파일에서 다시 확인해서 올리는 작업을 해야된다는 건데, 상대적으로 작은 메모리를 점유하는 Method 영역이 그럴 필요가 없을 것이라고 생각해서 입니다.   

  다시 자료를 읽으면서 생각해보니 컴파일 과정에서 에러를 잡고, 코드는 범위가 적은 만큼 프로그램 중간에 다시 읽어도 되는게 아닌가 싶기도 합니다. (또는 똑똑한 클래스로더가 올려야 되는 항목을 별도로 저장할 수도 있겠죠..?)  
  
- 객체의 선언/할당에 따른 메모리 변화 
    - 객체 선언시 : stack 에 참조 변수만 생성  
    `Human h = null;`
    - 객체 할당시 : heap 에 객체가 생성되며 참조 변수에 연결됩니다.  
    `h = new Human();`

### 참고 자료
https://programmer-seva.tistory.com/72
