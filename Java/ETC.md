# ETC
Java 공부를 하면서 알게된, 하지만 분류하기 애매한 것들을 모아두었습니다.

## Shallow Copy vs Deep Copy [링크](https://github.com/Hyune-c/TIL/blob/master/Java/Copy.md)

| Method             | Primitive Type Copy | Non-Primitive Type Copy | Speed   |
| ------------------ | ------------------- | ----------------------- | ------- |
| System.arraycopy() | Swallow             | Swallow                 | Fastest |
| Object.clone()     | Swallow             | Swallow                 | Fast    |
| Arrays.copyOf()    | Swallow             | Swallow                 | Fast    |
| Using for          | Depend on code      | Depend on code          | Slow    |

## Print Address [링크](https://github.com/Hyune-c/TIL/blob/master/Java/Print%20Address.md)