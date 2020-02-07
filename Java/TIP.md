# TIP

공부를 하면서 분류하기 애매하지만 유용하다고 생각되는 실수와 잡기술(?) 을 정리하였습니다.

## 변수 다루기
### 매개 변수에서 변수를 계산할 때
- 변수의 자료형에 따라 (3/2 = 1.0) 으로 계산되면서 의도하지 않은 결과가 나왔습니다.
- 매개 변수로 들어가기 전에 변수를 계산하여 저장하는 방식을 추천합니다.
```java
Math.ceil(1.5) = 2.0            // 의도한 결과
Math.ceil(3 / 2) = 1.0          // ??

Math.ceil((double) 3 / 2) = 2.0 // 매개 변수로 들어간 값을 casting 해서 해결  
```

### 변수의 크기를 비교해서 할당할 때
```java
// 가장 일반적인 방법
if (curDistance > maxDistance) maxDistance = curDistance;  
             
// 삼항 연산자를 활용한 방법
maxDistance = (curDistance > maxDistance) ? curDistance : maxDistance;

// 가장 깔끔한 방법  
maxDistance = Math.max(curDistance, maxDistance);                     
```

## Working...

this.numsQueue = new PriorityQueue<Integer>(new Comparator<Integer>() {  
  public int compare(Integer w1, Integer w2) {  
    return w2.compareTo(w1);  
  }  
});