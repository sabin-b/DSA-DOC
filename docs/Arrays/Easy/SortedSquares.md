# Sorted Squares

[Problem Link](https://leetcode.com/problems/squares-of-a-sorted-array/submissions/1934638103/){:target="_blank" rel="noopener noreferrer"}

### Description

Given an integer array `nums` sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

### Time Complexity & Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)


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

console.log(sortedSquares([-4, -1, 0, 3, 10]));
```
