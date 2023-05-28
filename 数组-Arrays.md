# Chapter 1 - Arrays

## 💡Basic Knowledge Points



***

## 📘Related Problems

### 15. Binary Search

* LeetCode Link:https://leetcode.com/problems/binary-search/

| Nth  | Time Cost | Pass/Not |
| ---- | --------- | -------- |
| 1    | 15mins    | ==Not==  |

#### ❌Mistakes Reflection

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

**📍Related Knowledge**: Operator precedence

* '++' / '--'  >  '*' / '\ ' / '%'  >  '+' / '-'  >  '<<' / '>>' > '+=' / '-=' / ' *=' ....

***

### 27. Remove Element 

* Leetcode: https://leetcode.com/problems/remove-element/description/

| Nth  | Time Cost | Pass/Not |
| ---- | --------- | -------- |
| 1    | 9 mins    | Pass     |

***

#### 📍Related Knowledge: Two Pointers

* Intro: 通过一个fast pointer 和 slow pointer， 完成double “for‘ loop 的工作
* 
<img width="549" alt="Screenshot 2023-05-28 at 4 40 17 PM" src="https://github.com/TomasZhu0321/Leetcode-Thomas/assets/90658084/671348cd-85a8-46a9-a82d-f46f8ad4be77">

  

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

  

