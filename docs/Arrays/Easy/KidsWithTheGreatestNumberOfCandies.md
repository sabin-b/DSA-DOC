# Kids With the Greatest Number of Candies

[Problem Link](https://leetcode.com/problems/kids-with-the-greatest-number-of-candies/){:target="_blank" rel="noopener noreferrer"}

### Description

There are `n` kids with candies. You are given an integer array `candies`, where each `candies[i]` represents the number of candies the `ith` kid has, and an integer `extraCandies`, denoting the number of extra candies that you have.

Return a boolean array `result` of length `n`, where `result[i]` is `true` if, after giving the `ith` kid all the `extraCandies`, they will have the **greatest** number of candies among all the kids, or `false` otherwise.

Note that **multiple** kids can have the **greatest** number of candies.

!!! example "Test Cases"

    **Example 1:**
    Input: candies = [2, 3, 5, 1, 3], extraCandies = 3
    Output: [true, true, true, false, true]
    Explanation: Kid with 5 is max. 2+3≥5 ✓, 3+3≥5 ✓, 5+3≥5 ✓, 1+3<5 ✗, 3+3≥5 ✓

    **Example 2:**
    Input: candies = [4, 2, 1, 1, 2], extraCandies = 1
    Output: [true, false, false, false, false]

    **Example 3:**
    Input: candies = [12, 1, 12], extraCandies = 10
    Output: [true, false, true]

### Approach 1: Brute Force

- **Time Complexity:** O(n²)
- **Space Complexity:** O(n)

For each kid, check if adding `extraCandies` makes their total greater than or equal to every other kid's candies.

```typescript
function kidsWithCandies(candies: number[], extraCandies: number): boolean[] {
  let n = candies.length;
  let result = new Array(n);
  for (let i = 0; i < candies.length; i++) {
    let greatest = true;
    let maxCandies = candies[i] + extraCandies;
    for (let j = 0; j < candies.length; j++) {
      if (candies[j] > maxCandies) {
        greatest = false;
        break;
      }
    }
    result[i] = greatest;
  }
  return result;
}

console.log(kidsWithCandies([2, 3, 5, 1, 3], 3)); // [true, true, true, false, true]
console.log(kidsWithCandies([4, 2, 1, 1, 2], 1)); // [true, false, false, false, false]
```

### Approach 2: One Pass

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

First find the maximum number of candies any kid has. Then for each kid, check if their candies plus `extraCandies` is at least the max.

```typescript
function kidsWithCandies(candies: number[], extraCandies: number): boolean[] {
  let n = candies.length;
  let maxCandies = 0;
  for (let i = 0; i < n; i++) {
    if (candies[i] > maxCandies) {
      maxCandies = candies[i];
    }
  }
  let result = new Array(n);
  for (let j = 0; j < n; j++) {
    if (candies[j] + extraCandies >= maxCandies) {
      result[j] = true;
    } else {
      result[j] = false;
    }
  }

  return result;
}

console.log(kidsWithCandies([2, 3, 5, 1, 3], 3)); // [true, true, true, false, true]
console.log(kidsWithCandies([4, 2, 1, 1, 2], 1)); // [true, false, false, false, false]
```
