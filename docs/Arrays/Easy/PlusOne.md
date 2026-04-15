# Plus One

[Problem Link](https://leetcode.com/problems/plus-one/){:target="_blank" rel="noopener noreferrer"}

### Description

You are given a large integer represented as an integer array `digits`, where each `digits[i]` is the `i`th digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading zero's.

Increment the large integer by one and return the resulting array of digits.

!!! example "Test Cases"

    **Example 1:**
    Input: digits = [1, 2, 3]
    Output: [1, 2, 4]
    Explanation: The array represents 123. Incrementing by one gives 124.

    **Example 2:**
    Input: digits = [1, 2, 9]
    Output: [1, 3, 0]
    Explanation: The array represents 129. Incrementing by one gives 130.

    **Example 3:**
    Input: digits = [9, 9, 9]
    Output: [1, 0, 0, 0]
    Explanation: The array represents 999. Incrementing by one gives 1000.

### Approach: Single Pass from Right to Left

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

We process the digits from right to left (least significant digit). For each digit:
1. Add 1 to the current digit
2. If the result is less than 10, we're done - return the array
3. If the result is 10, set it to 0 and continue to the next digit

If we finish the loop and still haven't returned, it means all digits were 9s (like 999 → 1000), so we prepend a 1.

```typescript
function plusOne(digits: number[]): number[] {
  if (!Array.isArray(digits) || !digits.length) return [];
  
  for (let i = digits.length - 1; i >= 0; i--) {
    digits[i]++;
    if (digits[i] < 10) return digits;
    digits[i] = 0;
  }
  digits.unshift(1);
  return digits;
}

console.log(plusOne([1, 2, 3]));       // [1, 2, 4]
console.log(plusOne([1, 2, 9]));      // [1, 3, 0]
console.log(plusOne([9, 9, 9]));      // [1, 0, 0, 0]
```

### Explanation

- Start from the last digit and add 1
- If there's no carry (digit < 10), return immediately
- If there's a carry (digit becomes 10), set to 0 and continue
- After processing all digits, if we still have a carry, prepend 1 (handles cases like 999 → 1000)