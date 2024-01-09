
題目網址：[Leaf-Similar Trees - LeetCode](https://leetcode.com/problems/leaf-similar-trees/?envType=daily-question&envId=2024-01-09)
## 問題

#### 題目大綱

>Consider all the leaves of a binary tree, from left to right order, the values of those leaves form a **leaf value sequence**_._

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/16/tree.png)

>For example, in the given tree above, the leaf value sequence is `(6, 7, 4, 9, 8)`.
  Two binary trees are considered _leaf-similar_ if their leaf value sequence is the same.
  Return `true` if and only if the two given trees with head nodes `root1` and `root2` are leaf-similar.

###### 1
![](https://assets.leetcode.com/uploads/2020/09/03/leaf-similar-1.jpg)

**Input:** root1 = [3,5,1,6,2,9,8,null,null,7,4], root2 = [3,5,1,6,7,4,2,null,null,null,null,null,null,9,8]
**Output:** true
###### 2
![](https://assets.leetcode.com/uploads/2020/09/03/leaf-similar-2.jpg)

**Input:** root1 = [1,2,3], root2 = [1,3,2]
**Output:** false
## 解法

這個問題是要比較每個樹的末端值是否相同，相同就回傳true
用dfs將樹搜尋一次後將末端的值記錄起來再比較就可以了

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def dfs(self, root, value):
        if root is None:
            return

        if root.left is None and root.right is None:
            value.append(root.val)

        self.dfs(root.left, value)
        self.dfs(root.right, value)
        return

    def leafSimilar(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> bool:
        left = []
        right = []
        self.dfs(root1, left)
        self.dfs(root2, right)
        return left == right
```

#leetcode #tree #dfs 