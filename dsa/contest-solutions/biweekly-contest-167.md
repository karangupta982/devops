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

---

## Q2 — Longest Fibonacci Subarray (4 Points)
```python

class Solution:
    def longestSubarray(self, nums: List[int]) -> int:
        maxLen = 2
        si = 2
        summ = nums[0]+nums[1]
        n = len(nums)
        for i in range(2,n):
            if summ == nums[i]:
                si += 1
            else:
                si = 2
            maxLen = max(maxLen,si)
            summ = nums[i-1] + nums[i]
        
        return maxLen
        
````

---

## Q3 — Design Exam Scores Tracker (5 Points)
```python

from bisect import bisect_left

class ExamTracker:

    def start_ind(self, vec: list, st: int)->int:
        l=0
        r = len(vec)-1
        while l<=r:
            mid = l + (r-l)//2
            if vec[mid][0] >= st:
                r = mid-1
            else:
                l = mid+1
        return l

    def end_ind(self, vec:list, et:int)->int:
        l = 0
        r = len(vec)-1
        while l<=r:
            mid = l + (r-l)//2
            if vec[mid][0] > et :
                r = mid-1
            else:
                l = mid+1
        return r

    
    def __init__(self):
        self.vec = []
        self.prefix = []

    def record(self, time: int, score: int) -> None:
        
        pos = bisect_left(self.vec,(time,0))
        self.vec.insert(pos,(time,score))

        if not self.prefix:
            self.prefix.append(score)
        else:
            insert_val = score if pos == 0 else self.prefix[pos-1] + score
            self.prefix.insert(pos, insert_val)
            for i in range(pos+1,len(self.prefix)):
                self.prefix[i] = self.prefix[i] + score

    def totalScore(self, st: int, et: int) -> int:
        
        if not self.vec:
            return 0

        si = self.start_ind(self.vec,st)
        li = self.end_ind(self.vec,et)

        if(si>li or li<0 or si >= len(self.vec) ):
            return 0
        
        total = self.prefix[li] - (0 if si==0 else self.prefix[si-1])
        return total

        
````