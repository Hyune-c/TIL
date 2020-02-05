# 전략 패턴 Strategy Pattern

- 전략 패턴 (strategy pattern) 은 실행 중에 알고리즘을 선택할 수 있게 하는 행위 소프트웨어 디자인 패턴입니다. 
- 특정한 계열의 알고리즘들을 정의하고 각 알고리즘을 캡슐화하며 이 알고리즘들을 해당 계열 안에서 상호 교체가 가능하게 만듭니다.
- 전략은 알고리즘을 사용하는 클라이언트와는 독립적으로 다양하게 만듭니다. 

### 문제 상황
- 서로 다른 성격을 가진 자식 클래스를 다수 생성하여야 합니다.
- 서로 다른 자식 클래스들은 메소드를 공유할 수도, 하지 않을 수도 있습니다.

### 실패한 해결 방법
> 클래스 상속을 활용하는 경우

- 부모 클래스의 메소드를 모든 자식 클래스가 동일하게 사용할 수 있습니다.
	- 서로 다른 자식 클래스가 같은 메소드를 사용하게 됨으로 의도하지 않은 동작을 할 수 있습니다.

> 인터페이스를 활용하는 경우

- 인터페이스의 모든 메소드를 필수적으로 오버로딩을 해야합니다.  
따라서 해당 메소드가 필요 없는 자식 클래스도 불필요한 오버로딩을 하게 됩니다.
- 같은 기능을 하는 메소드도 중복하여 작성해야 됩니다.
- 상속보다는 구성을 활용한다.

### 디자인 원칙
- 애플리케이션에서 달라지는 부분을 찾아내고, 달라지지 않는 부분으로부터 분리시킨다.
- 구현이 아닌 인터페이스에 맞춰서 프로그래밍한다.

### 구현 방법
부모 클래스는 자식 클래스들이 공통적으로 사용하는 메소드와 이 메소드의 행동 전략을 가지고 있는 인터페이스 (이하 전략 클래스) 를 상태 값으로 가지고 있습니다.
1. 디자인 원칙에 따라 분리된 애플리케이션의 구성에 맞는 인터페이스를 정의하고 이를 상속받아 전략 클래스를 구현합니다.
2. 상태 값에 전략 클래스를 할당합니다.
3. 실행한 클래스는 할당된 전략 클래스에 맞는 행동을 하게 됩니다.  
이를 위해서 생성자 또는 set 메소드를 사용합니다.

### 샘플 코드
![img](https://user-images.githubusercontent.com/55722186/73810682-8e2ec200-481a-11ea-94e1-347464562d79.png)
```java
public class MiniDuckSimulator {
    public static void main(String[] args) {
        MallardDuck mallard = new MallardDuck(); // Quack : Quack, Fly : can fly

        FlyBehavior cantFly = () -> System.out.println("I can't fly");
        QuackBehavior squeak = () -> System.out.println("Squeak");

        RubberDuck rubberDuckie = new RubberDuck(cantFly, squeak); // Quack : Squeak, Fly : can't fly
        DecoyDuck decoy = new DecoyDuck(); // Quack : Silence, Fly : can't fly

        Duck model = new ModelDuck(); // Quack : Quack, Fly : can't fly

        mallard.performQuack(); // Quack
        rubberDuckie.performQuack(); // Squeak
        decoy.performQuack(); // Silence

        System.out.println();

        model.performFly(); // can't fly
        model.setFlyBehavior(new FlyRocketPowered()); // flyBehavior = FlyRocketPowered
        model.performFly(); // flying with a rocket
    }
}
```


```java
public class MiniDuckSimulator1 {
   public static void main(String[] args) {
      Duck mallard = new MallardDuck(); // Quack : Quack, Fly : can fly
      mallard.performQuack(); // Quack
      mallard.performFly(); // flying

      System.out.println();

      Duck model = new ModelDuck(); // Quack : Quack, Fly : can't fly
      model.performFly(); // can't fly
      model.setFlyBehavior(new FlyRocketPowered()); // flyBehavior = FlyRocketPowered
      model.performFly(); // flying with a rocket
   }
}
```

## 마치며..
- 캡슐화된 패턴을 할당하고 지속적으로 변경해야 됨으로 네이밍이 중요할 것 같습니다.
- 예시 코드에는 set, get 메소드가 존재함에도 lamda 를 통한 메소드를 생성하여 대입, 만들어진 클래스를 직접 대입, set 메소드를 이용한 할당을 하였습니다. 
여기에 대한 추가 공부는 spring 을 배우는 시점에 다시 할 예정입니다.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzOTIyMTk2MTMsMTc1NTUwNTU4M119
-->