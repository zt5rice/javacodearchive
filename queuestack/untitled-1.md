# 31. Queue By Two Stacks

Medium

Java: Implement a queue by using two stacks. The queue should provide size\(\), isEmpty\(\), offer\(\), poll\(\) and peek\(\) operations. When the queue is empty, poll\(\) and peek\(\) should return null.

C++: Implement a queue by using two stacks. The queue should provide size\(\), isEmpty\(\), push\(\), front\(\) and pop\(\) operations. When the queue is empty, front\(\) should return -1.

**Assumptions**

* The elements in the queue are all Integers.
* size\(\) should return the number of elements buffered in the queue.
* isEmpty\(\) should return true if there is no element buffered in the queue, false otherwise.

```text
public class Solution {
    private LinkedList<Integer> in;
    private LinkedList<Integer> out;

  public Solution() {
    // Write your solution here.
    in = new LinkedList<Integer>();
    out = new LinkedList<Integer>();
  }
  
  public Integer poll() {
        // if outstack is empty,
        // need to move the elements from in stack to out stack
        move();
        return out.isEmpty() ? null : out.pollFirst();
  }
  
  public void offer(int value) {
        // always push into the int stack
        in.offerFirst(value);
  }
  
  public Integer peek() {
        // always push into the in stack
        move();
        return out.isEmpty() ? null : out.peekFirst();
  }

  private void move() {
    if(out.isEmpty()) {
      while (!in.isEmpty()) {
        out.offerFirst(in.pollFirst());
      }
    }
  }
  
  public int size() {
    return in.size() + out.size();
  }
  
  public boolean isEmpty() {
    return in.size() == 0 && out.size() == 0;
  }
}
```

