Stream 은 Java 8 에 추가된 Lambda 를 활용할 수 있는 기술 중 하나로, `연속된 요소의 집합` 을 순차 처리합니다.  
병렬 처리를 통해 성능을 향상시킬 수도 있지만 몇 가지 주의 사항이 있습니다.

| Stream 의 특징 |                                                  |
| -------------- | ------------------------------------------------ |
| No storage     | 별도의 저장 공간이 필요하지 않습니다             |
| Immutable      | 원본을 수정하지 않고 결과를 생성합니다           |
| Laziness       | 결과를 위한 최소한의 동작만을 수행합니다         |
| Possibly       | 무한한 값을 가질 수 있습니다                     |
| Consumable     | 스트림의 요소는 생명 주기 동안 한번만 사용됩니다 |

---

# 병렬 처리, Parallelism

> Stream 의 병렬 처리는 `데이터 병렬성` 을 구현한 것으로, 내부적으로는 `Fork-Join Framework` 를 이용합니다.

## 사용하면 좋은 경우

- `충분한 개수의 가용 코어`와 `충분히 큰 요소당 처리 시간`
  
  - 처리 시간이 Thread Pool 과 Thread 생성의 오버헤드보다 클 때

- 비지니스 로직에 대한 충분한 이해도를 가졌을 때

- 요소의 순서에 의존하지 않는 연산

  - Bad Case 이더라도 순서를 포기하는 unordered() 를 통해 빠른 연산이 가능합니다.
  
    |      | Case                               |
    | ---- | ---------------------------------- |
    | Good | findAny(), allMatch(), noneMatch() |
    | Bad  | limit(), findFirst(), distinct()   |

- Fork 에 적절한 소스
  
    |      | Case                   | Description                                                     |
    | ---- | ---------------------- | --------------------------------------------------------------- |
    | Good | ArrayList              | 랜덤 엑세스 지원<br>Spliterator() 를 적절히 구현할 수 있는 경우 |
    | Bad  | LinkedList             | 랜덤 엑세스 미지원                                              |
    |      | HashSet, TreeSet       | 요소의 분리가 어려움                                            |
    |      | BufferedReader.lines() | 전체 요소의 수를 알지 못함                                      |

## 주의점

- 무한 Stream 은 과도한 리소스 점유를 유발할 수 있습니다.
- 각 스레드에서 서브 데이터를 처리하고 Join 과정에서 reduce() 연산이 일어납니다.
  - Primitive Type Stream 을 통해 Boxing(), UnBoxing() 의 낭비를 막을 수 있습니다.
- 결과의 길이를 예측할 수 없는 중간 연산이 있는 경우 적절한 Fork 가 되지 않을 수 있습니다.

---

> Reference

- 데이터 병렬성
  - 전체 데이터를 쪼개 서브 데이터들로 만들고, 각 서브 데이터들을 병렬 처리합니다.
- Fork-Join Framework
  - 분할 정복 알고리즘의 형태로 서브 데이터를 만들고, 멀티 코어에 할당하여 처리합니다.
  - ExecutorService 의 구현체인 ForkJoinPool 을 통해 스레드를 관리합니다.
- [https://yongho1037.tistory.com/705](https://yongho1037.tistory.com/705)
