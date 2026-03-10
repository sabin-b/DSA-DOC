# Find Most Frequent Vowel and Consonant

[Problem Link](https://leetcode.com/problems/find-most-frequent-vowel-and-consonant/description/)

### Description

You are given a string `s` consisting of lowercase English letters.

You must find the sum of the following values:

- The frequency of the most frequent vowel in `s`.
- The frequency of the most frequent consonant in `s`.

The vowels are 'a', 'e', 'i', 'o', and 'u'.

### Test Cases

**Example 1:**

Input: s = "successes"
Output: 6
Explanation:
The vowels are: 'u' (frequency 1), 'e' (frequency 2). The maximum frequency is 2.
The consonants are: 's' (frequency 4), 'c' (frequency 2). The maximum frequency is 4.
The output is 2 + 4 = 6.

**Example 2:**

Input: s = "aeiaeia"
Output: 3
Explanation:
The vowels are: 'a' (frequency 3), 'e' ( frequency 2), 'i' (frequency 2). The maximum frequency is 3.
There are no consonants in s. Hence, maximum consonant frequency = 0.
The output is 3 + 0 = 3.

### Approach 1: Using a Map

- **Time Complexity:** O(n)
- **Space Complexity:** O(k), where k is the number of unique characters in the string.

```typescript
function maxFreqSumAp1(s: string): number {
  let maxVowel = 0;
  let maxConsonants = 0;
  const lettersInfo = new Map<string, number>();
  for (const l of s) {
    if (!lettersInfo.has(l)) lettersInfo.set(l, 1);
    else lettersInfo.set(l, lettersInfo.get(l)! + 1);
  }
  const set = new Set(["a", "e", "i", "o", "u"]);
  lettersInfo.forEach((v, k) => {
    if (set.has(k)) maxVowel = Math.max(maxVowel, v);
    else maxConsonants = Math.max(maxConsonants, v);
  });
  return maxVowel + maxConsonants;
}

console.log(maxFreqSumAp1("successes")); // 6
console.log(maxFreqSumAp1("aeiaeia")); // 3
```

### Approach 2: Using an Array as a Frequency Counter

- **Time Complexity:** O(n)
- **Space Complexity:** O(1), since the array size is fixed at 26.

```typescript
function maxFreqSum(s: string): number {
  const freq = new Array(26).fill(0);
  const vowels = new Set(["a", "e", "i", "o", "u"]);

  let maxVow = 0;
  let maxCons = 0;

  for (let i = 0; i < s.length; i++) {
    const idx = s.charCodeAt(i) - 97;

    freq[idx]++;

    if (vowels.has(s[i])) {
        maxVow = Math.max(maxVow, freq[idx]);
    } else {
        maxCons = Math.max(maxCons, freq[idx]);
    }
  }
  return maxVow + maxCons;
}

console.log(maxFreqSum("successes")); // 6
console.log(maxFreqSum("aeiaeia")); // 3
```