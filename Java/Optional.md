# Optional
- 'T'타입의 객체를 포장해 주는 래퍼 클래스 (Wrapper class) 입니다.
    - 모든 타입의 참조 변수를 저장할 수 있습니다.
- 제공되는 메소드로 예상치 못한 NullPointerException 예외를 간단히 회피할 수 있습니다.

| 메소드                                                 | 설명                                                         |
| :----------------------------------------------------- | :----------------------------------------------------------- |
| static Optional empty()                                | 아무런 값도 가지지 않는 비어있는 Optional 객체를 반환함.     |
| T get()                                                | Optional 객체에 저장된 값을 반환함.                          |
| boolean isPresent()                                    | 저장된 값이 존재하면 true를 반환하고, 값이 존재하지 않으면 false를 반환함. |
| static Optional of(T value)                            | null이 아닌 명시된 값을 가지는 Optional 객체를 반환함.       |
| static Optional ofNullable(T value)                    | 명시된 값이 null이 아니면 명시된 값을 가지는 Optional 객체를 반환하며, 명시된 값이 null이면 비어있는 Optional 객체를 반환함. |
| T orElse(T other)                                      | 저장된 값이 존재하면 그 값을 반환하고, 값이 존재하지 않으면 인수로 전달된 값을 반환함. |
| T orElseGet(Supplier<? extends T> other)               | 저장된 값이 존재하면 그 값을 반환하고, 값이 존재하지 않으면 인수로 전달된 람다 표현식의 결괏값을 반환함. |
| T orElseThrow(Supplier<? extends X> exceptionSupplier) | 저장된 값이 존재하면 그 값을 반환하고, 값이 존재하지 않으면 인수로 전달된 예외를 발생시킴. |

