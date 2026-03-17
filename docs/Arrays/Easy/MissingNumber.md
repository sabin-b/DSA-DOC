# Missing Number

[Problem Link](https://leetcode.com/problems/missing-number/)

### Description

Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return the only number in the range that is missing from the array.

!!! example "Test Cases"

    **Example 1:**
    Input: nums = [3,0,1]
    Output: 2
    Explanation: n = 3 since there are 3 numbers, so the range is [0,3]. 2 is the missing number in the range since it does not appear in nums.

    **Example 2:**
    Input: nums = [0,1]
    Output: 2
    Explanation: n = 2 since there are 2 numbers, so the range is [0,2]. 2 is the missing number in the range since it does not appear in nums.

    **Example 3:**
    Input: nums = [9,6,4,2,3,5,7,0,1]
    Output: 8
    Explanation: n = 9 since there are 9 numbers, so the range is [0,9]. 8 is the missing number in the range since it does not appear in nums.

### Approach 1: Summation Formula (Gauss's Formula)

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

This elegant approach leverages a mathematical formula. We know the array should contain all numbers from `0` to `n`. We can calculate the expected sum of this full range using the Gauss's formula: `(n * (n + 1)) / 2`.

We then iterate through the input array to find its actual sum. The difference between the expected sum and the actual sum gives us the missing number.

```typescript
function missingNumber(nums: number[]): number {
  let n = nums.length;
  // Calculate the expected sum of numbers from 0 to n
  let expectedSum = (n * (n + 1)) / 2;

  // Calculate the actual sum of the numbers in the array
  let actualSum = 0;
  for (let i = 0; i < n; i++) {
    actualSum += nums[i];
  }

  // The difference is the missing number
  return expectedSum - actualSum;
}

console.log(missingNumber([3, 0, 1])); // 2
console.log(missingNumber([9, 6, 4, 2, 3, 5, 7, 0, 1])); // 8
```

### Approach 2: Bit Manipulation (XOR)

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

This is another clever approach that uses the properties of the XOR operator (`^`). The key properties are `x ^ x = 0` and `x ^ 0 = x`.

We can initialize a variable with `n` and then XOR it with every index and every value in the array. Since the numbers in the array will match an index from `0` to `n-1` (except for the missing one), all the present numbers will cancel themselves out, leaving only the missing number.

```typescript
function missingNumberXOR(nums: number[]): number {
  let result = nums.length;
  for (let i = 0; i < nums.length; i++) {
    result ^= i;
    result ^= nums[i];
  }
  return result;
}

console.log(missingNumberXOR([3, 0, 1])); // 2
console.log(missingNumberXOR([9, 6, 4, 2, 3, 5, 7, 0, 1])); // 8
```

This file is now ready to be added to your collection. Let me know if you need the `git` commands to commit it.

# Missing Number

[Problem Link](https://leetcode.com/problems/missing-number/)

### Description

Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return the only number in the range that is missing from the array.

!!! example "Test Cases"

    **Example 1:**
    Input: nums = [3,0,1]
    Output: 2
    Explanation: n = 3 since there are 3 numbers, so the range is [0,3]. 2 is the missing number in the range since it does not appear in nums.

    **Example 2:**
    Input: nums = [0,1]
    Output: 2
    Explanation: n = 2 since there are 2 numbers, so the range is [0,2]. 2 is the missing number in the range since it does not appear in nums.

    **Example 3:**
    Input: nums = [9,6,4,2,3,5,7,0,1]
    Output: 8
    Explanation: n = 9 since there are 9 numbers, so the range is [0,9]. 8 is the missing number in the range since it does not appear in nums.

### Approach 1: Summation Formula (Gauss's Formula)

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

This elegant approach leverages a mathematical formula. We know the array should contain all numbers from `0` to `n`. We can calculate the expected sum of this full range using the Gauss's formula: `(n * (n + 1)) / 2`.

We then iterate through the input array to find its actual sum. The difference between the expected sum and the actual sum gives us the missing number.

```typescript
function missingNumber(nums: number[]): number {
  let n = nums.length;
  // Calculate the expected sum of numbers from 0 to n
  let expectedSum = (n * (n + 1)) / 2;

  // Calculate the actual sum of the numbers in the array
  let actualSum = 0;
  for (let i = 0; i < n; i++) {
    actualSum += nums[i];
  }

  // The difference is the missing number
  return expectedSum - actualSum;
}

console.log(missingNumber([3, 0, 1])); // 2
console.log(missingNumber([9, 6, 4, 2, 3, 5, 7, 0, 1])); // 8
```

### Approach 2: Bit Manipulation (XOR)

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

This is another clever approach that uses the properties of the XOR operator (`^`). The key properties are `x ^ x = 0` and `x ^ 0 = x`.

We can initialize a variable with `n` and then XOR it with every index and every value in the array. Since the numbers in the array will match an index from `0` to `n-1` (except for the missing one), all the present numbers will cancel themselves out, leaving only the missing number.

```typescript
function missingNumberXOR(nums: number[]): number {
  let result = nums.length;
  for (let i = 0; i < nums.length; i++) {
    result ^= i;
    result ^= nums[i];
  }
  return result;
}

console.log(missingNumberXOR([3, 0, 1])); // 2
console.log(missingNumberXOR([9, 6, 4, 2, 3, 5, 7, 0, 1])); // 8
```
