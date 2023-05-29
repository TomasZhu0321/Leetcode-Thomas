# Chapter 1 - Arrays

##💡Basic Knowledge Points



***

##📘Related Problems

###15. Binary Search

* LeetCode Link:https://leetcode.com/problems/binary-search/

| Nth  | Time Cost | Pass/Not |
| ---- | --------- | -------- |
| 1    | 15mins    | ==Not==  |

####❌Mistakes Reflection

* My Code

  ```java
  class Solution {
      public int search(int[] nums, int target) {
          //trim
          if(nums[0] > target || nums[nums.length - 1] <target){
              return -1;
          }
          int left = 0;
          int right = nums.length - 1;
          while(left <= right){
              int mid = (right - left)>>1 + left; //❌ 
             // ✅int mid = ((right - left) >> 1) + left
              if(target > nums[mid]){
                  left = mid + 1;
              }else if(target < nums[mid]){
                  right = mid - 1;
              }
              else {
                  return mid;
              }
          }
          return -1; 
      }
  }
  ```

  

##### Q1: Why cannot break out of a "while" loop with a left-closed and right-closed condition?

A: Line 10, (right-left)>>1 need to add '( )'. In this case, if there is no ( ), the evaluation order would be : right - left => 1 + left => (right - left)  >> (1 + left)

**📍Related Knowledge **: ==Operator precedence==

* '++' / '--'  >  '*' / '\ ' / '%'  >  '+' / '-'  >  '<<' / '>>' > '+=' / '-=' / ' *=' ....

***

###27. Remove Element 

* Leetcode: https://leetcode.com/problems/remove-element/description/

| Nth  | Time Cost | Pass/Not |
| ---- | --------- | -------- |
| 1    | 9 mins    | Pass     |

***

####📍Related Knowledge: ==Two Pointeres==

* Intro: 通过一个fast pointer 和 slow pointer， 完成double “for‘ loop 的工作

* <img src="/Users/tomas/Library/Application Support/typora-user-images/Screenshot 2023-05-28 at 2.42.25 PM.png" alt="Screenshot 2023-05-28 at 2.42.25 PM" style="zoom:33%;" />

  

***

* My Code:

  ```Java
  class Solution {
      public int removeElement(int[] nums, int val) {
          int slow = 0;
          int fast = 0;
          for (; fast <= nums.length - 1; fast ++){
              if (nums[fast] != val){               
                  nums[slow] = nums[fast];
                  slow ++;
              }
          }
          return slow;
      }
  }
  ```


***

###977. Squares of a Sorted Array

* LeetCode: https://leetcode.com/problems/squares-of-a-sorted-array/

* My Idea:
  * Method: Two Pointers (Left and Right)
  * Specific: When nums[right] is higher than nums[left], exchange. 
  * ❓**Q1: But in this case, how to make sure the left pointer always point to the minimum? In other wrods, when to shift the left pointer? **
    * A：The problem is "Exchange". The right way should be **creating a new array** to store the compared value.

| Nth  | Time Cost            | Pass/Not |
| ---- | -------------------- | -------- |
| 1    | 24mins (After 5mins) | **Not**  |

* After checked the answer:

  ```java
  class Solution {
      public int[] sortedSquares(int[] nums) {
          int left = 0;
          int right = nums.length - 1;
          int [] result = new int[nums.length];
          int index = nums.length - 1;
          while(index >=0){
              if(nums[right]*nums[right] > nums[left]*nums[left]){
                  result[index] = nums[right]*nums[right];
                  right --;
              }else{
                  result[index] = nums[left]*nums[left];
                  left ++;
              }
              index --;
          }
          return result;
      }
  }
  ```

***

### 209. Minimum Size Subarray Sum

* LeetCode:https://leetcode.com/problems/minimum-size-subarray-sum/description/

| Nth  | Time Cost | Pass/Not |
| ---- | --------- | -------- |
| 1    | 35 mins   | Pass     |

* My Idea
  * Method: **Slide Window**
  * Specific: Two pointers. When sum < target, the right one keep increasing. Once sum >= target, the left one start shifting.
* Carl's Idea: https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0209.%E9%95%BF%E5%BA%A6%E6%9C%80%E5%B0%8F%E7%9A%84%E5%AD%90%E6%95%B0%E7%BB%84.md

* My Code:

  ```java
  class Solution {
      public int minSubArrayLen(int target, int[] nums) {
          int left = 0;
          int right = 0;
          int sum = nums[0];
          int size = Integer.MAX_VALUE;
          for (;left < nums.length; ){
              if(sum < target && right < nums.length -1){
                  right ++;
                  sum = sum + nums[right];
              }
              else if (sum >= target){
                 size = Math.min(right-left +1, size);
                 sum = sum - nums[left];
                 left ++;
              }
              else{
                  break;
              }
          }
          return size == Integer.MAX_VALUE ? 0 : size;
      }
  }
  ```

***

### 59. Spiral Matrix II

* Leetcode:https://leetcode.com/problems/spiral-matrix-ii/submissions/959814103/

| Nth  | Time Cost | Pass/Not |
| ---- | --------- | -------- |
| 1    | 47 mins   | Pass     |

My Code:

```java
class Solution {
    public int[][] generateMatrix(int n) {
        int [][] res = new int [n][n];
        int i = 0;
        int j = 0;
        int pointer = 1;
        for (int round = 0; round < n/2 ; round ++){
            i = round;
            j = round;
            // System.out.println("round:" + round);
            for(;j < n - 1 - round;){
                // System.out.println("i:" + i + ",j:" + j);
                res[i][j] = pointer;
                pointer ++;
                j ++;
            }
            System.out.println("**********");
            for(; i < n - 1 -round;){
                System.out.println("i:" + i + ",j:" + j);
                res[i][j] = pointer;
                pointer ++;
                i ++;
            }
            // System.out.println("**********");
            for(; j > round ;){
            //    System.out.println("i:" + i + ",j:" + j);
                res[i][j] = pointer;
                pointer ++;
                 j --;
            }
            // System.out.println("**********");
            for(; i > round ;){   
                // System.out.println("i:" + i + ",j:" + j);
                res[i][j] = pointer;
                pointer ++;
                i --; 
            }
        }
        if(n%2 == 1){
            res[n/2][n/2] = pointer ;
        }
        return res;
    }
}
```

