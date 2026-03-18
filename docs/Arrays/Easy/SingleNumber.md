# Single Number

[Problem Link](https://leetcode.com/problems/single-number/)

### Description

Given a non-empty array of integers `nums`, every element appears twice except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

!!! example "Test Cases"

    **Example 1:**
    Input: nums = [2,2,1]
    Output: 1

    **Example 2:**
    Input: nums = [4,1,2,1,2]
    Output: 4

    **Example 3:**
    Input: nums = [1]
    Output: 1

### Approach 1: Hash Map

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

This approach uses a hash map to store the frequency of each number in the array. We iterate through the array once to build the map. Then, we iterate through the array a second time to check the map and return the number that has a frequency of 1.

While this solution works correctly, it does not meet the follow-up constraint of using only constant extra space.

```typescript
function singleNumberWithMap(nums: number[]): number {
  let map: Record<number, number> = {};
  for (const num of nums) {
    map[num] = (map[num] || 0) + 1;
  }
  
  for (const num in map) {
    if (map[num] === 1) {
      return Number(num);
    }
  }
  return -1; // Should not be reached given the problem constraints
}

console.log(singleNumberWithMap([2, 2, 1])); // 1
console.log(singleNumberWithMap([4, 1, 2, 1, 2])); // 4
```

### Approach 2: Bit Manipulation (XOR)

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

This is the optimal solution that meets all the problem constraints. It leverages the properties of the XOR (`^`) bitwise operator:
1.  `x ^ x = 0` (XORing a number with itself results in zero).
2.  `x ^ 0 = x` (XORing a number with zero results in the number itself).

By XORing all the numbers in the array together, all the numbers that appear twice will cancel each other out (becoming 0), leaving only the single number.

```typescript
function singleNumber(nums: number[]): number {
  let xor = 0;
  for (const num of nums) {
    xor = xor ^ num;
  }
  return xor;
}

console.log(singleNumber([2, 2, 1])); // 1
console.log(singleNumber([4, 1, 2, 1, 2])); // 4
```


