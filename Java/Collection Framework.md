# Collection Framework 자료구조
<img src="https://user-images.githubusercontent.com/55722186/74129897-113d8700-4c24-11ea-83c2-6a1e6cc93c29.png" width="70%">

| Interface  |       | Desc                                                 | 구현 클래스                                      |
| ---------- | ----- | ---------------------------------------------------- | ------------------------------------------------ |
| Collection | List  | - 순서를 유지하고 저장 <br />- 중복 저장 기능        | - ArrayList <br />- Vector <br />- LinkedList    |
|            | Set   | - 순서를 유지하지 않고 저장 <br />- 중복 저장 안 됨  | - HashSet <br />- TreeSet                        |
|            | Queue | - FIFO(First In First Out) 구조                      | - ArrayDeque <br />- PriorityQueue               |
| Map        |       | - 키와 값의 쌍으로 저장 <br />- 키는 중복 저장 안 됨 | - HashMap, HashTable <br />- TreeMap, Properties |



## # TreeMap vs HashMap

|                             |       HashMap        |            TreeMap            |
| --------------------------- | :------------------: | :---------------------------: |
| Extends<br />Implementation | AbstractMap<br />Map | AbstractMap<br />NavigableMap |
| Null Key                    |         Yes          |              No               |
| Multiple Null Values        |         Yes          |              Yes              |
| <Key, Value> Order          |          No          |       Natural Ordering        |
| Synchronized                |          No          |              No               |
| Complexity                  |         O(1)         |            O(logN)            |

- HashMap 의 capacity (bucket) 이 충분히 커지는 경우 TreeMap 과 유사한 상태가 됩니다.
  - 공간배치를 다시하는 rehashing 을 할 수 있지만 큰 부하가 걸립니다.

- TreeMap 이 NullKey 를 가질 수 없는 이유
  - Key 가 Null 이면 ordering 시 NullPointerException 가 발생합니다.
    
## # LinkedHashMap
순서가 보장되는 HashMap

#### 주요 메소드
- LinkedHashMap (int initialCapacity, float loadFactor, boolean accessOrder)
    - (저장된 데이터의 수 > capacity * load_factor) 가 되면 rehasing 가 수행됩니다.
    - boolean accessOrder
        - true : 접근이 적은 순서대로 저장됩니다. (access-order)
        - false : 입력한 순서대로 저장됩니다. (insertion-order)            
- removeEldestEntry (Map.Entry<K,V> eldest)
    - 생성자의 accessOrder 값에 따라 가장 오래된 <K,V> 를 삭제 합니다.
- getOrDefault(Object key, V defaultValue)
    - Optional 을 대신할 수 있는 메소드로 key 를 찾지 못할 경우 defaultValue 를 리턴합니다.

#### 소스 코드
https://github.com/Hyune-c/algorithm/blob/master/src/main/java/leetcode/lrucache/Solution.java 

#### 참고 자료  
https://library1008.tistory.com/11

## 참고 자료
https://bit.ly/2uAcHLb
