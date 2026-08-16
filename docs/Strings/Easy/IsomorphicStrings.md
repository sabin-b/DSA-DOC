# Isomorphic Strings

[Problem Link](https://leetcode.com/problems/isomorphic-strings/description/){:target="_blank" rel="noopener noreferrer"}

### Description

Given two strings `s` and `t`, *determine if they are isomorphic*.

Two strings `s` and `t` are isomorphic if the characters in `s` can be replaced to get `t`.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

Constraints:
- `1 <= s.length <= 5 * 10^4`
- `t.length == s.length`
- `s` and `t` consist of any valid ASCII character.

!!! example "Test Cases"

    **Example 1:**
    Input: s = "egg", t = "add"
    Output: true
    Explanation: Mapping 'e' to 'a' and 'g' to 'd' makes both strings identical.

    **Example 2:**
    Input: s = "foo", t = "bar"
    Output: false
    Explanation: Both 'o' and 'f' would need to map to 'b'/'a' inconsistently.

    **Example 3:**
    Input: s = "paper", t = "title"
    Output: true

### Approach 1: Using Two Maps

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

Use two hash maps to track the mapping in both directions: `sMap` maps each character in `s` to its counterpart in `t`, and `tMap` maps each character in `t` to its counterpart in `s`. While iterating, if a character already has a mapping that conflicts with the current pair, return `false`. If the loop completes with no conflicts, return `true`.

```typescript
function isIsomorphicAp1(s: string, t: string): boolean {
  const sMap = new Map();
  const tMap = new Map();

  if (s.length !== t.length) {
    return false;
  }

  for (let i = 0; i < s.length; i++) {
    let sEl = s[i];
    let tEl = t[i];

    if (sMap.has(sEl) && sMap.get(sEl) !== tEl) {
      return false;
    } else if (tMap.has(tEl) && tMap.get(tEl) !== sEl) {
      return false;
    }

    sMap.set(sEl, tEl);
    tMap.set(tEl, sEl);
  }

  return true;
}

console.log(isIsomorphicAp1("egg", "add")); // true
console.log(isIsomorphicAp1("foo", "bar")); // false
console.log(isIsomorphicAp1("paper", "title")); // true
```
