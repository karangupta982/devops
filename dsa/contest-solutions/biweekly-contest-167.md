# LeetCode Biweekly Contest 167 — Python Solutions

**Contest Link:** [LeetCode Weekly Contest 167](https://leetcode.com/contest/biweekly-contest-167/)

This file contains all my Python solutions for Biweekly Contest 167, written with clear structure and consistent formatting.

---

## Q1 — Equal Score Substrings (3 Points)
```python

class Solution:
    def scoreBalance(self, s: str) -> bool:
        st = set()
        n = len(s)
        summ = 0

        for c in s:
            summ += (ord(c) - ord('a') + 1) 
            st.add(summ)

        if summ & 1:
            return False
        
        if (summ//2) in st:
            return True

        return False
        
````
