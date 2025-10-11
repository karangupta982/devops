# LeetCode Weekly Contest 470 — Python Solutions

**Contest Link:** [LeetCode Weekly Contest 470](https://leetcode.com/contest/weekly-contest-470/)

This file contains all my Python solutions for Weekly Contest 470, written with clear structure and consistent formatting.

---

## Q1 — Alternating Sum (3 Points)
```python
from typing import List

class Solution:
    def alternatingSum(self, nums: List[int]) -> int:
        n = len(nums)
        total = 0
        for i in range(n):
            total += nums[i] if i % 2 == 0 else -nums[i]
        return total


# Example usage
if __name__ == "__main__":
    sol = Solution()
    print(sol.alternatingSum([1, 2, 3, 4, 5]))  # Output: 3
````

---

## Q2 — Longest Subsequence (4 Points)

```python
from typing import List

class Solution:
    def longestSubsequence(self, nums: List[int]) -> int:
        xori = nums[0]
        n = len(nums)
        for i in range(1, n):
            xori ^= nums[i]

        if xori != 0:
            return n
        else:
            maxi = max(nums)
            if maxi == 0:
                return 0
            else:
                return n - 1


# Example usage
if __name__ == "__main__":
    sol = Solution()
    print(sol.longestSubsequence([1, 2, 3]))  # Output: 3
    print(sol.longestSubsequence([0, 0, 0]))  # Output: 0
```

---

## Q3 — Remove Substring (5 Points)

```python
class Solution:
    def removeSubstring(self, s: str, k: int) -> str:
        st = []
        for c in s:
            if st and st[-1][0] == c:
                st[-1] = (c, st[-1][1] + 1)
            else:
                st.append((c, 1))

            n = len(st)
            if n >= 2 and st[n-2][0] == '(' and st[n-2][1] >= k and st[n-1][0] == ')' and st[n-1][1] >= k:
                st[n-2] = (st[n-2][0], st[n-2][1] - k)
                st.pop()
                if st and st[-1][1] == 0:
                    st.pop()

        ans = ""
        for c, cnt in st:
            ans += c * cnt
        return ans


# Example usage
if __name__ == "__main__":
    sol = Solution()
    print(sol.removeSubstring("(((())))", 2))  # Example output
```

---
