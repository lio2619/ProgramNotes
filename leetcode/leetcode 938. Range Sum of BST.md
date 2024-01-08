題目網址：[LeetCode - The World's Leading Online Programming Learning Platform](https://leetcode.com/problems/range-sum-of-bst/submissions/)

## 問題

#### 題目大綱

>Given the `root` node of a binary search tree and two integers `low` and `high`, return _the sum of values of all nodes with a value in the **inclusive** range_ `[low, high]`.
#### 範例

###### 1
**Input:** root = [10,5,15,3,7,null,18], low = 7, high = 15
**Output:** 32
**Explanation:** Nodes 7, 10, and 15 are in the range [7, 15]. 7 + 10 + 15 = 32.

###### 2
**Input:** root = [10,5,15,3,7,13,18,1,null,6], low = 6, high = 10
**Output:** 23
**Explanation:** Nodes 6, 7, and 10 are in the range [6, 10]. 6 + 7 + 10 = 23.


## 解法

透過DFS去搜尋二元搜尋樹，將符合比low大同時比high小的數相加起來就是答案
因為是二元搜尋樹，所以如果目前的node.val比low小那就只需要搜尋右邊
因為是二元搜尋樹，所以如果目前的node.val比high大那就只需要搜尋左邊

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def __init__(self):
        self.ans = 0

    def dfs(self, currentNode, low, high):
        if currentNode is None:
            return

        if high >= currentNode.val >= low:
            self.ans += currentNode.val
            self.dfs(currentNode.left, low, high)
            self.dfs(currentNode.right, low, high)
        elif currentNode.val < low:
            self.dfs(currentNode.right, low, high)
        elif currentNode.val > high:
            self.dfs(currentNode.left, low, high)

        return

    def rangeSumBST(self, root: Optional[TreeNode], low: int, high: int) -> int:
        self.dfs(root, low, high)
        return self.ans
```

#leetcode #tree #dfs 