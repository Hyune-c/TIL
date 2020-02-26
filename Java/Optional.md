# Optional
- 'T'타입의 객체를 포장해 주는 래퍼 클래스 (Wrapper class) 입니다.
    - 모든 타입의 참조 변수를 저장할 수 있습니다.
- 제공되는 메소드로 예상치 못한 NullPointerException 예외를 간단히 회피할 수 있습니다.
- T get() (강제 Unwrapping) 은 사용을 지양합니다.
    - 존재하지 않는 경우 `NoSuchElementException` 를 반환하며, 이를 방지하는 orElse() 등의 메소드를 사용합니다.

| 메소드                                                 | 설명                                                         |
| :----------------------------------------------------- | :----------------------------------------------------------- |
| static Optional empty()                                | 빈 Optional 객체를 반환.                                     |
| T get()                                                | Optional 객체에 저장된 값을 반환.                            |
| boolean isPresent()                                    | 값의 존재를 반환.                                                             |
| static Optional of(T value)                            | 명시된 값의 Optional 객체를 반환.                            |
| static Optional ofNullable(T value)                    | 값이 null 이면 빈 Optional 객체를 반환.<br />값이 null 이 아니면 명시된 값의 Optional 객체를 반환. |
| T orElse(T other)                                      | 값이 존재하면 해당 값을 반환.<br />값이 존재하지 않으면 명시된 값을 반환. |
| T orElseGet(Supplier<? extends T> other)               | 값이 존재하면 해당 값을 반환.<br />값이 존재하지 않으면 인수로 전달된 람다 표현식의 결과값을 반환. |
| T orElseThrow(Supplier<? extends X> exceptionSupplier) | 값이 존재하면 해당 값을 반환.<br />값이 존재하지 않으면 인수로 전달된 예외를 발생. |

