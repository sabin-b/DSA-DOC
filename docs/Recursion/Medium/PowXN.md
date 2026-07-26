# Pow(x, n)

[Problem Link](https://leetcode.com/problems/powx-n/){:target="_blank" rel="noopener noreferrer"}

<!-- Date: 30/07/2026 -->

### Description

Implement `pow(x, n)`, which calculates `x` raised to the power `n` (i.e., `x^n`).

!!! example "Test Cases"

    **Example 1:**
    Input: x = 2.00000, n = 10
    Output: 1024.00000
    Explanation: 2^10 = 1024

    **Example 2:**
    Input: x = 2.10000, n = 3
    Output: 9.26100
    Explanation: 2.1^3 = 9.261

    **Example 3:**
    Input: x = 2.00000, n = -2
    Output: 0.25000
    Explanation: 2^(-2) = 1/(2^2) = 1/4 = 0.25

### Approach 1: Brute Force

- **Time Complexity:** O(n) - We iterate through n multiplications.
- **Space Complexity:** O(1) - Only a few variables used.

This approach directly multiplies x by itself n times.

- Handle negative exponents by converting to positive and taking reciprocal.
- Use the exponentiation operator for direct calculation.

```typescript
function myPow(x: number, n: number): number {
    if (n === 0) return 1;

    const exp = Math.abs(n);
    const ans = x ** exp;

    return n > 0 ? ans : 1 / ans;
}

console.log(myPow(2.00000, 10));   // 1024.00000
console.log(myPow(2.10000, 3));    // 9.26100
console.log(myPow(2.00000, -2));   // 0.25000
```

### Approach 2: Fast Exponentiation (Binary Method)

- **Time Complexity:** O(log n) - We halve n in each iteration.
- **Space Complexity:** O(1) - Only a few variables used.

This approach uses binary exponentiation to reduce the number of multiplications.

- Start with result = 1.
- While n > 0:
    - If n is odd, multiply result by x.
    - Square x.
    - Halve n (integer division).
- Handle negative exponents by taking reciprocal.

```typescript
function myPow(x: number, n: number): number {
  if (n === 0) return 1;

  if (n < 0) {
    x = 1 / x;
    n = Math.abs(n);
  }

  let result = 1;

  while (n > 0) {
    if (n % 2 === 1) {
      result *= x;
    }
    x *= x;
    n = Math.floor(n / 2);
  }

  return result;
}

console.log(myPow(2.00000, 10));   // 1024.00000
console.log(myPow(2.10000, 3));    // 9.26100
console.log(myPow(2.00000, -2));   // 0.25000
```

### Tips

- Any number raised to the power of 0 equals 1 (e.g., `2^0 = 1`).
- `n = Math.abs(n)` converts negative to positive and vice versa.
- Binary exponentiation reduces time from O(n) to O(log n) by halving the exponent each step.

### Question and Answer Flow

**Q1: Why do we return 1 when n is 0?**
Because any number raised to the power of 0 is defined as 1. This is the base case.

**Q2: How do we handle negative exponents?**
We convert x to 1/x and make n positive. For example, 2^(-3) = (1/2)^3 = 1/8.

**Q3: Why does the binary method check if n is odd?**
When n is odd, we need to multiply the result by the current x before squaring x and halving n.

**Q4: Why is fast exponentiation O(log n)?**
Because we halve n in each iteration, so we need at most log2(n) iterations.

**Q5: What happens if x is 0 and n is negative?**
This would result in division by zero, but the problem constraints ensure valid inputs.

### Mind Map

```mermaid
mindmap
  root((Pow(x, n)))
    Base Case
      n === 0
      Return 1
    Negative Exponent
      x = 1/x
      n = Math.abs(n)
    Brute Force
      Direct exponentiation
      Time O(n)
    Binary Method
      Check if n is odd
      Multiply result by x
      Square x
      Halve n
      Time O(log n)
    Tips
      x^0 = 1
      abs(n) for sign
```
