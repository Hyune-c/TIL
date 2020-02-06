# 메소드 Method

어떠한 특정 작업을 수행하기 위한 명령문의 집합
 
```java
public int add(int val) { 
  return 1;
}

접근한정자 리턴타입 메소드이름 ([매개변수]){
  실행할 코드....
}
```

### 매개 변수의 개수를 모르는 경우
매개 변수의 개수는 정해져 있는 경우가 일반적이지만, 어떤 상황에서는 메소드를 선언할 때 매개 변수의 개수를 알 수 없는 경우도 있습니다. 이런 경우 2가지 방법이 있습니다.

- 매개 변수를 배열로 받습니다.
- 매개 변수를 '...' 을 통해 받습니다.
	- 이 경우 내부적으로 매개 변수의 개수만큼 배열이 생성됩니다.
```java
public class sumTest {
  public int sum(int a, int b) {    // 매개 변수가 2개
    return a + b;
  }

  public int sum2(int[] arr) {      // 매개 변수가 배열
    return Arrays.stream(arr).sum();
  }

  public int sum3(int... arr) {    // 매개 변수의 개수를 알 수 없음
    return Arrays.stream(arr).sum();
  }

  public static void main(String[] args) {
    sumTest st = new sumTest();

    System.out.println(st.sum2(new int[]{1, 2, 3, 4, 5}));    // 15, OK
    System.out.println(st.sum3(1, 2, 3, 4, 5));               // 15, OK

    System.out.println(st.sum2(1, 2, 3, 4, 5));               // Compile Error
    System.out.println(st.sum3(new int[]{1, 2, 3, 4, 5}));    // 15, OK
  }
}
```



### 함수 vs 메소드

-   함수 : 함수는 독립적으로 존재하며, 로직 처리 후 결과를 반환합니다.
-   메소드 : 메서드는 클래스에 종속되어 존재하며, 해당 클래스에 대한 객체가 생성되어야 사용할 수 있습니다.
<!--stackedit_data:
eyJoaXN0b3J5IjpbODIxNjc2Mjc2XX0=
-->