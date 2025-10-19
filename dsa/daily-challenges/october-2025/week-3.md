
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
````

---

## Time & Space Complexity

* **Time Complexity:** O(n log n)
* **Space Complexity:** O(1)

````


---


# Date: 2025-10-19

## Problem
[LeetCode: 1625. Lexicographically Smallest String After Applying Operations](https://leetcode.com/problems/lexicographically-smallest-string-after-applying-operations?envType=daily-question&envId=2025-10-19)

---

## Code (Python)

```python

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

            arr = list(t)
            for i in range(1, n, 2):
                arr[i] = str((int(arr[i]) + a) % 10)
            added = ''.join(arr)

            if added not in seen:
                q.append(added)

            rotated = t[-b:] + t[:-b]
            if rotated not in seen:
                q.append(rotated)

        return ans
````

---

## Time & Space Complexity

* **Time Complexity:** O(n × 10 × n) ≈ O(n²) — due to rotation and BFS traversal
* **Space Complexity:** O(n × 10ⁿ) in worst case (all unique states)

````