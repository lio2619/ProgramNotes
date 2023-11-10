
題目網址：[Restore the Array From Adjacent Pairs - LeetCode](https://leetcode.com/problems/restore-the-array-from-adjacent-pairs/description/?envType=daily-question&envId=2023-11-10)

## 問題

#### 題目大綱

>There is an integer array `nums` that consists of `n` **unique** elements, but you have forgotten it. However, you do remember every pair of adjacent elements in `nums`.

>You are given a 2D integer array `adjacentPairs` of size `n - 1` where each `adjacentPairs[i] = [ui, vi]` indicates that the elements `ui` and `vi` are adjacent in `nums`.

>It is guaranteed that every adjacent pair of elements `nums[i]` and `nums[i+1]` will exist in `adjacentPairs`, either as `[nums[i], nums[i+1]]` or `[nums[i+1], nums[i]]`. The pairs can appear **in any order**.

>Return _the original array_ `nums`_. If there are multiple solutions, return **any of them**_.

###### 1
**Input:** adjacentPairs = [ [2, 1], [3, 4], [3, 2] ]
**Output:** [1,2,3,4]
**Explanation:** This array has all its adjacent pairs in adjacentPairs.
Notice that adjacentPairs[i] may not be in left-to-right order.
###### 2
**Input:** adjacentPairs = [ [4, -2], [1, 4], [-3, 1] ]
**Output:** [-2,4,1,-3]
**Explanation:** There can be negative numbers.
Another solution is [-3,1,4,-2], which would also be accepted.

###### 3
**Input:** adjacentPairs = [ [100000, -100000] ]
**Output:** [100000,-100000]
## 解法

題目說會給你二維的相鄰陣列
假設原本是這樣：[1,2,3,4]，那他就會給你這樣的陣列：[ [2, 1], [3, 4], [3, 2] ]
可以從中發現這個東西：{2: [1, 3], 1: [2], 3: [4, 2], 4: [3]}
而其中只有1、4這個數字只有一個相鄰的地方，代表他們是起點跟終點
可以從這兩點中的一點開始計算

比較詳細的請看一下這邊：[【Video】Give me 5 minutes - O(n) time and space - How we think about a solution - Restore the Array From Adjacent Pairs - LeetCode](https://leetcode.com/problems/restore-the-array-from-adjacent-pairs/solutions/4271506/video-give-me-5-minutes-o-n-time-and-space-how-we-think-about-a-solution/?envType=daily-question&envId=2023-11-10)

```python
def restoreArray(self, adjacentPairs: List[List[int]]) -> List[int]:
        graph = {} 

        for i, j in adjacentPairs:
            graph.setdefault(i, []).append(j)
            graph.setdefault(j, []).append(i)

        ans = []
        visit = set()
        stack = [next(l for l in graph if len(graph[l]) == 1)] 

        while stack:
            n = stack.pop()
            ans.append(n)
            visit.add(n)
            for m in graph[n]:
                if m not in visit:
                    stack.append(m)
        return ans
```

#leetcode #hash 