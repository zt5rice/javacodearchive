---
description: Medium
---

# 400. Rainbow Sort III

Given an array of balls with k different colors denoted by numbers 1- k, sort the balls.

**Examples**

* k=1, {1} is sorted to {1}
* k=3, {1, 3, 2, 1, 2} is sorted to {1, 1, 2, 2, 3}
* k=5, {3, 1, 5, 5, 1, 4, 2} is sorted to {1, 1, 2, 3, 4, 5, 5}

**Assumptions**

* The input array is not null.
* k is guaranteed to be &gt;= 1.
* k &lt;&lt; logn.

```text
public class Solution {
  public int[] rainbowSortIII(int[] array, int k) {
    if (array == null || array.length < 2) {
        return array;
    }
    int left = 0;
    int right = array.length - 1;
    for (int round = 1; round <= k / 2; round++) {
        // since leftColor + rightColor == k + 1
        int leftColor = round;
        int rightColor = k + 1 - round;
        for (int i = left; i <= right; i++) {
            if (array[i] == leftColor) {
                swap(array, i, left);
                left++;
            } else if (array[i] == rightColor) {
                swap(array, i, right);
                i--;
                right--;
            }
        }
    }
    return array;
  }

  private void swap(int[] array, int left, int right) {
      int tmp = array[left];
      array[left] = array[right];
      array[right] = tmp;
  }
}

```

