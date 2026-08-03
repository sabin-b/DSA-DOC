# Is Subsequence

[Problem Link](https://leetcode.com/problems/is-subsequence/description/){:target="_blank" rel="noopener noreferrer"}

### Description

Given two strings `s` and `t`, return `true` if `s` is a subsequence of `t`, or `false` otherwise.

A subsequence is a sequence that can be derived from another sequence by deleting some or no elements without changing the order of the remaining elements. For example, `"ace"` is a subsequence of `"abcde"` (delete `'b'` and `'d'`), but `"aec"` is not.

!!! example "Test Cases"

    Example 1:
    Input: s = "abc", t = "ahbgdc"
    Output: true
    Explanation: "abc" can be formed by deleting 'h' and 'd' from "ahbgdc", preserving order.

    Example 2:
    Input: s = "axc", t = "ahbgdc"
    Output: false
    Explanation: 'x' and 'c' appear out of order, so "axc" is not a subsequence.

### Approach 1: Two Pointers (Backward Scan)

- Time Complexity: O(n) where n is the length of t
- Space Complexity: O(1)

Scan `t` from right to left with a pointer `j` while matching characters of `s` from right to left with pointer `index`. Every match decrements `index`. If all characters of `s` were matched, `index` becomes `-1` and we return `true`. This is the mirror of the standard forward greedy scan.

```typescript
function isSubsequence(s: string, t: string): boolean {
  let index = s.length - 1;

  for (let j = t.length - 1; j >= 0; j--) {
    if (s[index] === t[j]) {
      index--;
    }
  }

  return index < 0 ? true : false;
}

console.log(isSubsequence("abc", "ahbgdc")); // true
console.log(isSubsequence("axc", "ahbgdc")); // false
```

### Approach 2: Two Pointers (Forward Scan)

- Time Complexity: O(n + m) where n is the length of s and m is the length of t
- Space Complexity: O(1)

Advance both pointers from the start: `i` points into `s` and `j` points into `t`. When characters match, move `i`. Always move `j`. If `i` reaches the end of `s`, every character was found in order.

```typescript
function isSubsequence(s: string, t: string): boolean {
  let i = 0;
  let j = 0;

  while (i < s.length && j < t.length) {
    if (s[i] === t[j]) i++;
    j++;
  }

  return i === s.length;
}

console.log(isSubsequence("abc", "ahbgdc")); // true
console.log(isSubsequence("axc", "ahbgdc")); // false
```
