# Jewels and Stones

[Problem Link](https://leetcode.com/problems/jewels-and-stones/)

### Description

You're given strings `jewels` representing the types of stones that are jewels, and `stones` representing the stones you have. Each character in `stones` is a type of stone you have. You want to know how many of the stones you have are also jewels.

Letters are case sensitive, so "a" is considered a different type of stone from "A".

!!! example "Test Cases"

    Example 1:
    Input: jewels = "aA", stones = "aAAbbbb"
    Output: 3

    Example 2:
    Input: jewels = "z", stones = "ZZ"
    Output: 0

### Approach 1: Brute Force

- Time Complexity: O(n\*m) where n is the length of stones and m is the length of jewels
- Space Complexity: O(1)

```typescript
/**
 * Approach: Brute Force
 * Time Complexity: O(n*m) where n is the length of stones and m is the length of jewels
 * Space Complexity: O(1)
 * You're given strings jewels representing the types of stones that are jewels, and stones representing the stones you have. Each character in stones is a type of stone you have. You want to know how many of the stones you have are also jewels. Letters are case sensitive, so "a" is considered a different type of stone from "A".
 * @param jewels
 * @param stones
 * @returns number of jewels in stones
 */
function numJewelsInStonesAp1(jewels: string, stones: string): number {
  let count = 0;
  for (let i = 0; i < stones.length; i++) {
    for (let j = 0; j < jewels.length; j++) {
      if (stones[i] === jewels[j]) {
        count++;
      }
    }
  }
  return count;
}

// jewels = "aA", stones = "aAAbbbb"
console.log(numJewelsInStonesAp1("aA", "aAAbbbb")); // 3
```

### Approach 2: Using HashTable (Set)

- Time Complexity: O(n + m)
- Space Complexity: O(m)

```typescript
/**
 * Approach - 2 (hastable)
 */
function numJewelsInStonesAp2(jewels: string, stones: string): number {
  let count = 0;
  let jewelsSet = new Set();
  for (const j of jewels) {
    jewelsSet.add(j);
  }
  for (const s of stones) {
    if (jewelsSet.has(s)) count++;
  }
  return count;
}

console.log(numJewelsInStonesAp2("aA", "aAAbbbb")); // 3
```
