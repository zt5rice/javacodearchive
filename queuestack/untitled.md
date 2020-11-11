# 280. Sort With 2 Stacks

Medium

Given an array that is initially stored in one stack, sort it with one additional stacks \(total 2 stacks\).

After sorting the original stack should contain the sorted integers and from top to bottom the integers are sorted in ascending order.

**Assumptions:**

* The given stack is not null.
* There can be duplicated numbers in the give stack.

**Requirements:**

* No additional memory, time complexity = O\(n ^ 2\).

```text
public class Solution {
  public void sort(LinkedList<Integer> s1) {
    // sanitory clean
    if(s1 == null || s1.size() <= 1) {
      return;
    }
    LinkedList<Integer> s2 = new LinkedList<Integer>();
    sort(s1, s2);
    // write a function with 2 Deque input: 
    // two deque: buffer top: sorted element; input
    // run several times sorting, each time record min val and count;
  }

  public void sort(Deque<Integer> input, Deque<Integer> buffer) {
    // two layers of while loop
    while(!input.isEmpty()) {     
      int curMin = Integer.MAX_VALUE;
      int count = 0;
      // first: find out the min and record count in each loop
      while(!input.isEmpty()){
        int cur = input.pollFirst();
        if (cur < curMin) {
          curMin = cur;
          count = 1; // why not 0;
        } else if (cur == curMin) {
          count++;
        }
        buffer.offerFirst(cur);
      }
      // second: return all elements except min element back to input deque
      while (!buffer.isEmpty() && buffer.peekFirst() >= curMin) {
        int tmp = buffer.pollFirst();
        if (tmp != curMin) {
          input.offerFirst(tmp);
        }
      }

      // if multiple times of curMin, add the rest back to buffer
      while (count-- > 0) {
        buffer.offerFirst(curMin);
      }
    }
    // put buffer element back to input deque; 
    while (!buffer.isEmpty()) {
      input.offerFirst(buffer.pollFirst());
    }
  }
}
```

