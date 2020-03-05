# TIP

### # 변수 다루기
#### 매개 변수에서 변수를 계산할 때
- 변수의 자료형에 따라 (3/2 = 1.0) 으로 계산되면서 의도하지 않은 결과가 나왔습니다.
- 변수를 계산하여 명시적으로 표기한 후 매개변수로 사용하는 방식을 권장합니다.
```java
Math.ceil(1.5) = 2.0            // 의도한 결과
Math.ceil(3 / 2) = 1.0          // 3 / 2 = 1.0 (not 1.5)

Math.ceil((double) 3 / 2) = 2.0 // 매개 변수로 들어간 값을 casting 해서 해결  
```

#### 변수의 크기를 비교해서 할당할 때
```java
// 가장 일반적인 방법
if (curDistance > maxDistance) maxDistance = curDistance;  
// 삼항 연산자를 활용한 방법
maxDistance = (curDistance > maxDistance) ? curDistance : maxDistance;
// 가장 깔끔한 방법  
maxDistance = Math.max(curDistance, maxDistance);                     
```

### # 문자열, 배열
#### 같은 문자가 정해진 길이의 문자열을 만들어야 되는 경우
- StringBuilder 로 만드는 것이 보통이겠지만, 아래와 같이 만드는 방법도 있습니다. 
 
```java
System.out.println(monster + " : " + "-".repeat(monster.getDistance()));
movedDistance = new String(new char[moveBehavior.getMoveCount(roundCount)]).replace("\0", "-");
movedDistance = (Stream.generate(() -> "-").limit(moveBehavior.getMoveCount(roundCount))).collect(Collectors.joining());
```

### # ETC
#### 실행 시간 구하기
```java
long start = System.currentTimeMillis();
/* 실행할 코드 */
long end = System.currentTimeMillis();
System.out.println("실행 시간(ms) : " + (end - start) / 1000.0);
```

#### HashMap 의 value 를 count 로 사용하기 위한 Override 
```java
class MyHashMap extends HashMap<Character, Integer> {
  @Override
  public Integer put(Character key, Integer value) {
    if (super.containsKey(key)) return super.put(key, super.get(key) + 1);
    return super.put(key, value);
  }

  @Override
  public Integer remove(Object key) {
    if (super.containsKey(key) && super.get(key) != 1)
      return super.put((char) key, super.get(key) - 1);
    return super.remove(key);
  }
}
```


### # Working...


```java
this.numsQueue = new PriorityQueue<Integer>(new Comparator<Integer>() {  
  public int compare(Integer w1, Integer w2) {  
    return w2.compareTo(w1);  
  }  
});
```
