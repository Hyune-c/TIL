# JavaBean
JavaBean API Specification 에 따른 Standard 로 POJO 와 아래 조건을 만족하여야됩니다.

- 모든 필드는 private 이며, getter/setter 메소드를 통해서만 접근 가능합니다.
- Argument 가 없는 생성자가 존재합니다.
- java.io.Serializable 인터페이스를 구현합니다.
    - Serializable 은 마커 인터페이스입니다.

```java
import java.io.Serializable;

public class SomeBean implements Serializable {

    private String beanName;

    public SomeBean() {
        // no-argument constructor
    }

    public String getBeanName() {
        return beanName;
    }

    public void setBeanName(String beanName) {
        this.beanName = beanName;
    }
}
```

> POJO 

순수한 자바 객체로 객체지향적인 원리에 충실하면서, 환경과 기술에 종속되지 않고 필요에 따라 재활용될 수 있는 방식으로 설계된 오브젝트를 말합니다.  
POJO 는 개념적인 것으로, 객체가 손상되지 않는다면 일부 변형을 허용합니다. (slightly breaks)

- 클래스 상속을 강제하지 않습니다. 
- 인터페이스 구현을 강제하지 않습니다. 
- 애노테이션 사용을 강제하지 않습니다.


## # 참고 자료 
- https://imasoftwareengineer.tistory.com/101
