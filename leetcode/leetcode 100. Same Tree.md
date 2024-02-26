
題目網址：[Same Tree - LeetCode](https://leetcode.com/problems/same-tree/description/?envType=daily-question&envId=2024-02-26)
## 問題

#### 題目大綱

>Given the roots of two binary trees `p` and `q`, write a function to check if they are the same or not.
   Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.


###### 1
![](https://assets.leetcode.com/uploads/2020/12/20/ex1.jpg)

**Input:** p = [1,2,3], q = [1,2,3]
**Output:** true
###### 2  
![](https://assets.leetcode.com/uploads/2020/12/20/ex2.jpg)

**Input:** p = [1,2], q = [1,null,2]
**Output:** false

###### 3
  
![](https://assets.leetcode.com/uploads/2020/12/20/ex3.jpg)

**Input:** p = [1,2,1], q = [1,1,2]
**Output:** false
## 解法

這個問題是要比較每個樹是否相同，相同就回傳true
用dfs將樹搜尋一次後將值記錄起來再比較就可以了

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
            value.append(None)
            return
            
        value.append(root.val)
        self.dfs(root.left, value)
        self.dfs(root.right, value)

        return

    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        one = []
        two = []
        self.dfs(p, one)
        self.dfs(q, two)

        return one == two
```

#leetcode #tree #dfs 