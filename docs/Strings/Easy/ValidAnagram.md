# Valid Anagram

[Problem Link](https://leetcode.com/problems/valid-anagram/description/){:target="_blank" rel="noopener noreferrer"}

### Description

Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

Constraints:
- `1 <= s.length, t.length <= 5 * 10^4`
- `s` and `t` consist of lowercase English letters.

!!! example "Test Cases"

    Example 1:
    Input: s = "anagram", t = "nagaram"
    Output: true

    Example 2:
    Input: s = "rat", t = "car"
    Output: false

### Approach 1: Brute Force

- Time Complexity: O(n log n)
- Space Complexity: O(n)

Sort both strings and compare them. If both strings contain the same characters, their sorted versions will be identical.

```typescript
function isAnagramAp1(s: string, t: string): boolean {
  if (s.length !== t.length) {
    return false;
  }

  return s.split("").sort().join("") === t.split("").sort().join("");
}

console.log(isAnagramAp1("anagram", "nagaram")); // true
console.log(isAnagramAp1("rat", "car")); // false
```

### Approach 2: Using a Map

- Time Complexity: O(n)
- Space Complexity: O(n)

Count the frequency of every character in both strings using two maps, then compare the counts of each character.

```typescript
function isAnagramAp2(s: string, t: string): boolean {
  if (s.length !== t.length) {
    return false;
  }

  let tMap = new Map();
  let sMap = new Map();

  for (let i = 0; i < s.length; i++) {
    sMap.set(s[i], (sMap.get(s[i]) ?? 0) + 1);
    tMap.set(t[i], (tMap.get(t[i]) ?? 0) + 1);
  }

  for (let j = 0; j < t.length; j++) {
    if (sMap.get(s[j]) !== tMap.get(s[j])) {
      return false;
    }
  }
  return true;
}

console.log(isAnagramAp2("anagram", "nagaram")); // true
console.log(isAnagramAp2("rat", "car")); // false
```
