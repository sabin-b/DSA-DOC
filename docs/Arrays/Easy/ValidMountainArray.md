# Valid Mountain Array

[Problem Link](https://leetcode.com/problems/valid-mountain-array/){:target="_blank" rel="noopener noreferrer"}

### Description

Given an integer array `arr`, return `true` if `arr` is a valid mountain array.

A valid mountain array `arr` must satisfy the following conditions:
- `arr.length >= 3`
- There exists some `i` with `0 < i < arr.length - 1` such that:
  - `arr[0] < arr[1] < ... < arr[i - 1] < arr[i]`
  - `arr[i] > arr[i + 1] > ... > arr[arr.length - 1]`

In other words, the array must strictly increase to a peak, then strictly decrease.

!!! example "Test Cases"

    **Example 1:**
    Input: arr = [2, 1]
    Output: false
    Explanation: The array has fewer than 3 elements, so it cannot be a valid mountain.

    **Example 2:**
    Input: arr = [3, 5, 5]
    Output: false
    Explanation: The array has a plateau (equal adjacent elements) instead of strictly increasing to the peak.

    **Example 3:**
    Input: arr = [0, 3, 2, 1]
    Output: true
    Explanation: The array strictly increases from 0 to 3 (peak), then strictly decreases from 3 to 1.

### Approach 1: Two-Pass Scan

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

This approach scans the array in two phases:
1. **Climbing phase:** Walk uphill while each element is greater than the next.
2. **Descending phase:** Walk downhill while each element is greater than the next.

A valid mountain must have at least one climb and one descent (requires at least 3 elements), and the peak cannot be at the start or end of the array.

```typescript
function validMountainArray(arr: number[]): boolean {
  // Return false for invalid input
  if (!Array.isArray(arr) || !arr.length) return false;

  let n = arr.length;
  // A valid mountain must have at least 3 elements
  if (n < 3) return false;

  let index = 0;

  // Climbing phase: walk up while the array is increasing
  while (index + 1 < n && arr[index] < arr[index + 1]) {
    index++;
  }

  // Peak cannot be at the first or last position
  if (index === 0 || index === n - 1) return false;

  // Descending phase: walk down while the array is decreasing
  while (index + 1 < n && arr[index] > arr[index + 1]) {
    index++;
  }

  // If we reached the end, it's a valid mountain
  return index === n - 1;
}

console.log(validMountainArray([2, 1])); // false
console.log(validMountainArray([3, 5, 5])); // false
console.log(validMountainArray([0, 3, 2, 1])); // true
```
