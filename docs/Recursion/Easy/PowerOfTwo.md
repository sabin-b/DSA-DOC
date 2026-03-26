# Power of Two

[Problem Link](https://leetcode.com/problems/power-of-two/)

### Description

Given an integer `n`, return `true` if it is a power of two. Otherwise, return `false`.

An integer `n` is a power of two if there exists an integer `x` such as `n == 2^x`.

!!! example "Test Cases"

    **Example 1:**
    Input: n = 1
    Output: true
    Explanation: 2^0 = 1

    **Example 2:**
    Input: n = 16
    Output: true
    Explanation: 2^4 = 16

    **Example 3:**
    Input: n = 3
    Output: false

### Approach 1: Recursion

- **Time Complexity:** O(log n) - The input `n` is halved in each recursive call.
- **Space Complexity:** O(log n) - The recursion depth is proportional to log n, which is stored on the call stack.

This approach uses the definition of a power of two to break the problem down.
- **Base Cases:**
    - If `n` is 1, it is the base power of two (2^0), so we return `true`.
    - If `n` is less than 1 (i.e., 0 or negative) or if `n` is not divisible by 2, it cannot be a power of two, so we return `false`.
- **Recursive Step:** If the number passes the initial checks, we know it's a positive, even number. We can then test if `n / 2` is a power of two by calling the function recursively.

```typescript
function powerOfTwo(n: number): boolean {
  // Base Case 1: 1 is a power of two (2^0)
  if (n === 1) {
    return true;
  }
  
  // Base Case 2: Numbers less than 1 or odd numbers (other than 1) are not powers of two.
  if (n < 1 || n % 2 !== 0) {
    return false;
  }
  
  // Recursive Step: Divide by 2 and check again.
  return powerOfTwo(n / 2);
}

console.log(powerOfTwo(16)); // true
console.log(powerOfTwo(5));  // false
console.log(powerOfTwo(1));  // true
```

### Approach 2: Bit Manipulation

- **Time Complexity:** O(1)
- **Space Complexity:** O(1)

This is a highly efficient and clever trick. A number is a power of two if it has exactly one '1' bit in its binary representation.
- `n = 8` is `1000` in binary.
- `n - 1 = 7` is `0111` in binary.

When we perform a bitwise AND (`&`) between `n` and `n-1`, the result will be `0` if and only if `n` is a power of two. We also must check that `n > 0`, since the logic doesn't apply to zero or negative numbers.

```typescript
function powerOfTwoBitwise(n: number): boolean {
  // A power of two must be positive and have only one bit set to 1.
  return n > 0 && (n & (n - 1)) === 0;
}

console.log(powerOfTwoBitwise(16)); // true
console.log(powerOfTwoBitwise(5));  // false
console.log(powerOfTwoBitwise(1));  // true
```
