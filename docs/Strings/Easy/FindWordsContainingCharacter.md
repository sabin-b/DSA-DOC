# Find Words Containing Character

[Problem Link](https://leetcode.com/problems/find-words-containing-character/description/)

### Description

You are given a 0-indexed array of strings words and a character x.

Return an array of indices representing the words that contain the character x.

Note that the returned array may be in any order.

!!! example "Test Cases"

     Example 1:
     Input: words = ["leet","code"], x = "e"
     Output: [0,1]
     Explanation: "e" occurs in both words: "leet", and "code". Hence, we return indices 0 and 1.

      Example 2:
     Input: words = ["abc","bcd","aaaa","cbc"], x = "a"
     Output: [0,2]
     Explanation: "a" occurs in "abc", and "aaaa". Hence, we return indices 0 and 2.

      Example 3:
     Input: words = ["abc","bcd","aaaa","cbc"], x = "z"
     Output: []
     Explanation: "z" does not occur in any of the words. Hence, we return an empty array.

### Approach 1: Using nested loop

- Time Complexity: O(n^2)
- Space Complexity: O(1)

```typescript
function findWordsContaining(words: string[], x: string): number[] {
  let res = [];
  for (let i = 0; i < words.length; i++) {
    let w = words[i];
    let found = false;
    for (let j = 0; j < w.length; j++) {
      if (w[j] === x) {
        found = true;
        break;
      }
    }
    if (found) {
      res.push(i);
    }
  }
  return res;
}

console.log(findWordsContaining(["leet", "code"], "e")); // [0, 1]
```
