# Check If N and Its Double Exist

[Problem Link](https://leetcode.com/problems/check-if-n-and-its-double-exist/){:target="_blank" rel="noopener noreferrer"}

### Description

Given an array `arr` of integers, check if there exist two indices `i` and `j` such that:

- `arr[i] == 2 * arr[j]`
- OR `arr[j] == 2 * arr[i]`

Return `true` if such pair exists, `false` otherwise.

!!! example "Test Cases"

    **Example 1:**
    Input: arr = [10, 2, 5, 10]
    Output: true
    Explanation: arr[0] = 10 is double of arr[2] = 5.

    **Example 2:**
    Input: arr = [3, 1, 7, 11]
    Output: false
    Explanation: No number is double of another.

    **Example 3:**
    Input: arr = [0, 0]
    Output: true
    Explanation: 0 * 2 = 0, so both elements are doubles of each other.

### Solution

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

Use a Set to track numbers we've seen. For each number, check if its double or half (if even) exists in the set.

```typescript
function checkIfExist(arr: number[]): boolean {
  if (!Array.isArray(arr) || !arr.length) return false;
  const set = new Set<number>();
  for (const n of arr) {
    if (set.has(n * 2) || (n % 2 === 0 && set.has(n / 2))) return true;
    set.add(n);
  }
  return false;
}

console.log(checkIfExist([10, 2, 5, 10])); // true
console.log(checkIfExist([3, 1, 7, 11])); // false
console.log(checkIfExist([0, 0]));         // true
```

### Explanation

- Handle edge cases: empty or non-array input returns false
- Iterate through array, for each number check:
  - If double exists in set → return true
  - If number is even and half exists in set → return true
- Add current number to set for future comparisons
- Return false if no valid pair found

| Approach | Time | Space |
|----------|------|-------|
| Set | O(n) | O(n) |