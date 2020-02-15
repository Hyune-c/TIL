# ETC
Java 공부를 하면서 알게된, 하지만 분류하기 애매한 것들을 모아두었습니다.

## Shallow Copy vs Deep Copy [링크](https://github.com/Hyune-c/TIL/blob/master/Java/Copy.md)

| Method             | Primitive Type Copy | Non-Primitive Type Copy | Speed   |
| ------------------ | ------------------- | ----------------------- | ------- |
| System.arraycopy() | Deep                | Shallow                 | Fastest |
| Object.clone()     | Deep                | Shallow                 | Fast    |
| Arrays.copyOf()    | Deep                | Shallow                 | Fast    |
| Using for          | Depend on code      | Depend on code          | Slow    |

## Print Address [링크](https://github.com/Hyune-c/TIL/blob/master/Java/Print%20Address.md)

## private final vs private final static
#### private final
재할당할 수 없으며 사용하기 위해서는 인스턴스 선언이 필요합니다.

#### private static final
재할당할 수 없으며 메모리에 한 번 올라가면 프로그램 전체에서 공유합니다.

> private static final 을 사용해야 되는 이유

private 한 경우 해당 클래스에서만 사용 되는 값이므로 인스턴스가 생성될 때마다 선언/할당 되는 낭비를 할 필요가 없습니다.

#### 참고 자료
https://zorba91.tistory.com/275