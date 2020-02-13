# Print Address in Java
**많은 내용이 검증되지 않았습니다. 도움 부탁드립니다.**

## 불가능하다.

`There is no way to get the memory address of anything in Java. All that is hidden by the JVM`

하지만 hashCode() 와 identityHashCode() 를 통해 유사한 고유 값(?)을 가져올 수 있습니다.

```java
### tmp
hashCode() : 762218386
identityHashCode() : 762218386
hashCode() (HEX) : 2d6e8792
toString : test$Temp@2d6e8792

### tmp2
hashCode() : 249515771
identityHashCode() : 249515771
hashCode() (HEX) : edf4efb
toString : test$Temp@edf4efb
```

```java
import java.util.Arrays;

public class test {
  public static class Temp {
    public int a;

    public Temp(int a) {
      this.a = a;
    }
  }

  public static void printAddress(Temp tmp, String tmpString) {
    System.out.println("### " + tmpString);
    System.out.println("hashCode() : " + tmp.hashCode());
    System.out.println("identityHashCode() : " + System.identityHashCode(tmp));
    System.out.println("hashCode() (HEX) : " + Integer.toHexString(tmp.hashCode()));
    System.out.println("toString : " + String.valueOf(tmp));
    System.out.println();
  }

  public static void main(String[] args) {
    Temp tmp = new Temp(50);
    Temp tmp2 = new Temp(50);

    printAddress(tmp, "tmp");
    printAddress(tmp2, "tmp2");
  }
}
```

## 참고 자료
https://stackoverflow.com/questions/33315184/how-to-print-address-of-a-variable-in-java