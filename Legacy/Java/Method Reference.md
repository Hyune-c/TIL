# Method Reference 메소드 참조
- 람다 표현식이 단 하나의 메소드만을 호출하는 경우에 불필요한 매개변수를 제거하고 사용할 수 있도록 해줍니다.
    - 불필요한 매개변수를 제거하고 '::' 기호를 사용하여 표현할 수 있습니다.

```java    
monsters.stream().forEach(System.out::println);
```

https://www.geeksforgeeks.org/double-colon-operator-in-java/