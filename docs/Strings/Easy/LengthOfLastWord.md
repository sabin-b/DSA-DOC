# Length of Last Word

[Problem Link](https://leetcode.com/problems/length-of-last-word/description/){:target="_blank" rel="noopener noreferrer"}

### Description
Given a string s consisting of words and spaces, return the length of the last word in the string.
A word is a maximal substring consisting of non-space characters only.

!!! example "Test Cases"

    Example 1:
    Input: s = "Hello World"
    Output: 5
    Explanation: The last word is "World" with length 5.

    Example 2:
    Input: s = "   fly me   to   the moon  "
    Output: 4
    Explanation: The last word is "moon" with length 4.

    Example 3:
    Input: s = "luffy is still joyboy"
    Output: 6
    Explanation: The last word is "joyboy" with length 6.

### Approach 1: Using double loop

- Time Complexity: O(n)
- Space Complexity: O(1)

```typescript
function lengthOfLastWord(s: string): number {
  let count = 0;
  let i = s.length - 1;

  while (i > 0 && s[i] === " ") {
    i--;
  }

  while (i > 0 && s[i] !== " ") {
    count++;
    i--;
  }
  return count;
}
console.log(lengthOfLastWord("Hello World")); // 5
```

### Approach 2: Using single loop

- Time Complexity: O(n)
- Space Complexity: O(1)

```typescript
function lengthOfLastWord(s: string): number {
  let count = 0;
  let i = s.length - 1;
  while (i >= 0) {
    if (s[i] !== " ") {
      count++;
    } else if (count > 0) {
      break;
    }
    i--;
  }
  return count;
}
console.log(lengthOfLastWord("Hello World")); // 5
```