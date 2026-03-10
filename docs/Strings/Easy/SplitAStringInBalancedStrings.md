# Split a String in Balanced Strings

[Problem Link](https://leetcode.com/problems/split-a-string-in-balanced-strings/description/)

### Description

Balanced strings are those that have an equal quantity of 'L' and 'R' characters.

Given a balanced string `s`, split it into some number of substrings such that:

- Each substring is balanced.

Return the maximum number of balanced strings you can obtain.

!!! example "Test Cases"

    **Example 1:**
    Input: s = "RLRRLLRLRL"
    Output: 4
    Explanation: s can be split into "RL", "RRLL", "RL", "RL", each substring contains same number of 'L' and 'R'.

    **Example 2:**
    Input: s = "RLRRRLLRLL"
    Output: 2
    Explanation: s can be split into "RL", "RRRLLRLL", since each substring contains an equal number of 'L' and 'R'

    **Example 3:**
    Input: s = "LLLLRRRR"
    Output: 1
    Explanation: s can be split into "LLLLRRRR".

### Approach 1: Single Pass with a Balance Counter

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

This approach uses a single counter, `temp`, to keep track of the balance between 'R' and 'L' characters. We increment for 'R' and decrement for 'L'. Whenever the counter returns to zero, we know we've found a balanced substring.

```typescript
function balancedStringSplit(s: string): number {
  let temp = 0;
  let count = 0;
  for (let i = 0; i < s.length; i++) {
    if (s[i] === "R") {
      temp++;
    } else {
      temp--;
    }

    if (temp === 0) {
      count++;
    }
  }
  return count;
}

console.log(balancedStringSplit("RLRRLLRLRL")); // 4
console.log(balancedStringSplit("RLRRRLLRLL")); // 2
console.log(balancedStringSplit("LLLLRRRR")); // 1
```

### Approach 2: Using Separate 'L' and 'R' Counters

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

This approach uses two separate counters, `L` and `R`, to track the counts of each character. When the counts are equal (and non-zero), we've found a balanced substring and can increment our result.

```typescript
function balancedStringSplitAp2(s: string): number {
  let R = 0;
  let L = 0;
  let count = 0;
  for (let i = 0; i < s.length; i++) {
    if (s[i] === "R") {
      R++;
    } else {
      L++;
    }

    if (R === L) {
      count++;
    }
  }
  return count;
}

console.log(balancedStringSplitAp2("RLRRLLRLRL")); // 4
console.log(balancedStringSplitAp2("RLRRRLLRLL")); // 2
console.log(balancedStringSplitAp2("LLLLRRRR")); // 1
```
