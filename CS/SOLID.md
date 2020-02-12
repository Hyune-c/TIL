# SOLID 객체 지향 설계

### Single responsibility principle 단일 책임 원칙 

한 클래스는 하나의 책임만 가져야 한다. 

### Open/closed principle 개방-폐쇄 원칙
소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.

### Liskov substitution principle 리스코프 치환 원칙
프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다.
계약에 의한 설계를 참고하라. 

### Interface segregation principle 인터페이스 분리 원칙
특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다

### Dependency inversion principle 의존관계 역전 원칙
추상화에 의존해야지, 구체화에 의존하면 안된다.  
의존성 주입은 이 원칙을 따르는 방법 중 하나다. 

