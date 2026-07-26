# Find Numbers with Even Number of Digits

[Problem Link](https://leetcode.com/problems/find-numbers-with-even-number-of-digits/description/){:target="_blank" rel="noopener noreferrer"}

### Description

Given an array `nums` of integers, return how many of them contain an **even number of digits**.

!!! example "Test Cases"

    **Example 1:**
    Input: nums = [12, 345, 2, 6, 7896]
    Output: 2
    Explanation: 12 has 2 digits (even), 345 has 3 digits (odd), 2 has 1 digit (odd), 6 has 1 digit (odd), 7896 has 4 digits (even). Only 12 and 7896 have even digit counts.

    **Example 2:**
    Input: nums = [555, 901, 482, 1771]
    Output: 1
    Explanation: Only 1771 has an even number of digits.

    **Example 3:**
    Input: nums = [12, 16, 19, 21]
    Output: 4
    Explanation: All numbers have exactly 2 digits.

### Approach 1: Convert to String

- **Time Complexity:** O(n \* k) where k is the average number of digits
- **Space Complexity:** O(k) for the string conversion

Convert each number to a string and check if its length is even.

```typescript
function findNumbers(nums: number[]): number {
  let result = 0;

  for (let i = 0; i < nums.length; i++) {
    if (nums[i].toString().length % 2 === 0) result++;
  }

  return result;
}

console.log(findNumbers([12, 345, 2, 6, 7896])); // 2
console.log(findNumbers([555, 901, 482, 1771])); // 1
console.log(findNumbers([12, 16, 19, 21]));      // 4
```

### Approach 2: Count Digits with Division

- **Time Complexity:** O(n \* k) where k is the average number of digits
- **Space Complexity:** O(1)

Use repeated division by 10 to count digits without string conversion.

```typescript
function countDigits(n: number): number {
  let digits = 0;
  while (n > 0) {
    digits++;
    n = Math.floor(n / 10);
  }
  return digits;
}

function findNumbers(nums: number[]): number {
  let result = 0;
  for (let i = 0; i < nums.length; i++) {
    const count = countDigits(nums[i]);
    if (count % 2 === 0) result++;
  }
  return result;
}

console.log(findNumbers([12, 345, 2, 6, 7896])); // 2
console.log(findNumbers([555, 901, 482, 1771])); // 1
console.log(findNumbers([12, 16, 19, 21]));      // 4
```

### Tips

- An even number of digits means the digit count is divisible by 2, i.e. `count % 2 === 0`
- The minimum number with even digits starts at 2 digits (10, 11, ... 99)
