# TIP

개발을 하면서 아직 분류하지는 못했지만 유용하다고 생각되는 잡기술(?) 을 정리하였습니다.

this.numsQueue = new PriorityQueue<Integer>(new Comparator<Integer>() {  
  public int compare(Integer w1, Integer w2) {  
    return w2.compareTo(w1);  
  }  
});