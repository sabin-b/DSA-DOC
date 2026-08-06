# First Unique Character in a String

[Problem Link](https://leetcode.com/problems/first-unique-character-in-a-string/description/){:target="_blank" rel="noopener noreferrer"}

### Description

Given a string `s`, find the **first** non-repeating character in it and return its index. If it **does not** exist, return `-1`.

- `1 <= s.length <= 10^5`
- `s` consists of only lowercase English letters.

!!! example "Test Cases"

    **Example 1:**
    Input: s = "leetcode"
    Output: 0
    Explanation: The character 'l' at index 0 is the first character that does not occur at any other index.

    **Example 2:**
    Input: s = "loveleetcode"
    Output: 2

    **Example 3:**
    Input: s = "aabb"
    Output: -1

### Approach 1: Brute Force

- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)

For each character, count how many times it appears in the string by scanning the whole string. Return the index of the first character whose count is exactly 1.

```typescript
function firstUniqChar(s: string): number {
    let l = s.length;
    for (let i = 0; i < l; i++) {
        let count = 0;
        for (let j = 0; j < l; j++) {
            if (s[i] === s[j]) count++
        }
        if (count === 1) return i
    }
    return -1;
};

console.log(firstUniqChar("leetcode")); // 0
console.log(firstUniqChar("loveleetcode")); // 2
console.log(firstUniqChar("aabb")); // -1
```

### Approach 2: Using a Map

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

Count the frequency of every character in a single pass using a hash map. Then scan the string again and return the index of the first character with frequency 1. Space is O(1) because the string only contains lowercase English letters (at most 26 entries).

```typescript
function firstUniqChar(s: string): number {
  let lengthOfStr = s.length;
  let map: Record<string, number> = {};

  for (let i = 0; i < lengthOfStr; i++) {
    if (map[s[i]]) {
      map[s[i]] = map[s[i]] + 1;
    } else {
      map[s[i]] = 1;
    }
  }

  for (let j = 0; j < lengthOfStr; j++) {
    if (map[s[j]] && map[s[j]] === 1) return j;
  }

  return -1;
}

console.log(firstUniqChar("leetcode")); // 0
console.log(firstUniqChar("loveleetcode")); // 2
console.log(firstUniqChar("aabb")); // -1
```

### Approach 3: Frequency Array of 26

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

Since the string only contains lowercase English letters, use a fixed array of size 26 indexed by `charCodeAt(i) - 97` instead of a hash map. This avoids hashing overhead and keeps space strictly O(1).

```typescript
function firstUniqChar(s: string): number {
    const count = new Array(26).fill(0);
    for (let i = 0; i < s.length; i++) {
        count[s.charCodeAt(i) - 97]++;
    }
    for (let j = 0; j < s.length; j++) {
        if (count[s.charCodeAt(j) - 97] === 1) return j;
    }
    return -1;
}

console.log(firstUniqChar("leetcode")); // 0
console.log(firstUniqChar("loveleetcode")); // 2
console.log(firstUniqChar("aabb")); // -1
```
