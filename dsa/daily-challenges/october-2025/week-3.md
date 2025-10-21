# Date: 2025-10-18

## Problem

[LeetCode: Max Distinct Elements](https://leetcode.com/problems/maximum-number-of-distinct-elements-after-operations/description/?envType=daily-question&envId=2025-10-18)

---

## Code (Python)

```python
class Solution:
    def maxDistinctElements(self, nums: List[int], k: int) -> int:
        maxi = float('-inf')
        cnt = 0
        nums.sort()
        for num in nums:
            r1 = num - k
            r2 = num + k
            if maxi < r1:
                cnt += 1
                maxi = r1
            elif maxi >= r1 and maxi < r2:
                cnt += 1
                maxi += 1
        return cnt
```

---

## Time & Space Complexity

* **Time Complexity:** O(n log n)
* **Space Complexity:** O(1)

---

# Date: 2025-10-19

## Problem

[LeetCode: 1625. Lexicographically Smallest String After Applying Operations](https://leetcode.com/problems/lexicographically-smallest-string-after-applying-operations?envType=daily-question&envId=2025-10-19)

---

## Code (Python)

```python
from collections import deque

class Solution:
    def findLexSmallestString(self, s: str, a: int, b: int) -> str:
        seen = set()
        q = deque([s])
        ans = s
        n = len(s)

        while q:
            t = q.popleft()
            if t in seen:
                continue
            seen.add(t)

            ans = min(ans, t)

            # Add operation: add 'a' to all odd indices
            arr = list(t)
            for i in range(1, n, 2):
                arr[i] = str((int(arr[i]) + a) % 10)
            added = ''.join(arr)

            if added not in seen:
                q.append(added)

            # Rotate operation
            rotated = t[-b:] + t[:-b]
            if rotated not in seen:
                q.append(rotated)

        return ans
```

---

## Time & Space Complexity

* **Time Complexity:** O(n × 10 × n) ≈ O(n²) — due to rotation and BFS traversal
* **Space Complexity:** O(n × 10ⁿ) in worst case (all unique states)

---


# Date: 2025-10-19

## Problem

[LeetCode:  3346. Maximum Frequency of an Element After Performing Operations I](https://leetcode.com/problems/maximum-frequency-of-an-element-after-performing-operations-i?envType=daily-question&envId=2025-10-21)

---

## Code (Python)

```python

class Solution:
    def maxFrequency(self, nums: List[int], k: int, numOperations: int) -> int:
        maxi = max(nums)
        freq = [0]*(maxi+k+1)
        n = maxi+k+1
        for num in nums:
            freq[num]+=1
        for i in range(n):
            freq[i] += freq[i-1]
        
        ans = 1
        for target in range(1,n):
            l = max(0,target-k-1)
            r = min(n-1,target + k)
            repeat = freq[target] - freq[target-1] 
            diff = freq[r] - freq[l] - repeat
            diff = min(diff, numOperations) 
            ans = max(ans,diff+repeat)
        
        return ans

```

---

## Time & Space Complexity

* **Time Complexity:** O(n + maxi + k)
* **Space Complexity:** O(maxi + k)




        