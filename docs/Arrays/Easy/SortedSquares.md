# Sorted Squares

[Problem Link](https://leetcode.com/problems/squares-of-a-sorted-array/submissions/1934638103/){:target="\_blank" rel="noopener noreferrer"}

### Description

Given an integer array `nums` sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

!!! example "Test Cases"

    **Example 1:**
    Input: nums = [-4,-1,0,3,10]
    Output: [0,1,9,16,100]
    Explanation: After squaring, the array becomes [16,1,0,9,100]. After sorting, it becomes [0,1,9,16,100].

    **Example 2:**
    Input: nums = [-7,-3,2,3,11]
    Output: [4,9,9,49,121]

### Approach 1: Two Pointers

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

This approach uses a two-pointer technique to build the result array from largest to smallest. We compare the absolute values of the elements at the `left` and `right` pointers. The larger square is placed at the end of the `result` array, and the corresponding pointer is moved inward.

```typescript
function sortedSquares(nums: number[]): number[] {
  const n = nums.length;
  let left = 0;
  let right = n - 1;
  let index = n - 1;
  const result = new Array(n);
  while (left <= right) {
    let leftSq = Math.pow(Math.abs(nums[left]), 2);
    let rightSq = Math.pow(Math.abs(nums[right]), 2);

    if (leftSq > rightSq) {
      result[index] = leftSq;
      left++;
    } else {
      result[index] = rightSq;
      right--;
    }
    index--;
  }
  return result;
}

console.log(sortedSquares([-4, -1, 0, 3, 10])); // [0, 1, 9, 16, 100]
console.log(sortedSquares([-7, -3, 2, 3, 11])); // [4, 9, 9, 49, 121]
```
