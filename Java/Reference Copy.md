# Reference Copy
리터럴과 객체들을 복사할 때 헷갈리는 점에 대해 정리하였습니다. 

## Deep Copy vs Shallow Copy

| Method             | Primitive Type Copy | Non-Primitive Type Copy | Speed   |
| ------------------ | ------------------- | ----------------------- | ------- |
| System.arraycopy() | Swallow             | Swallow                 | Fastest |
| Object.clone()     | Swallow             | Deep                    | Fast    |
| Arrays.copyOf()    | Swallow             | Swallow                 | Fast    |
| Using for          | Depend on code      | Depend on code          | Slow    |

```java
import java.util.Arrays;

public class test {
  public static class Temp {
    public int a;
    public Object obj;

    public Temp(int a) {
      this.a = a;
      this.obj = new Object();
    }

    public int getA() {
      return a;
    }
  }

  public static void main(String[] args) {
    Temp[] origin = new Temp[]{new Temp(1), new Temp(2), new Temp(280), new Temp(1500), new Temp(40000)};

    Temp[] arrayCopy = new Temp[5];
    System.arraycopy(origin, 0, arrayCopy, 0, 5);
    Temp[] clone = origin.clone();
    Temp[] copyOf = Arrays.copyOf(origin, 5);
    Temp[] forCopy = new Temp[5];
    for (int i = 0; i < origin.length; i++) {
      forCopy[i] = new Temp(origin[i].getA());
    }
  }
}
```