題目網址：[LeetCode - The World's Leading Online Programming Learning Platform](https://leetcode.com/problems/count-nodes-equal-to-average-of-subtree/submissions/?envType=daily-question&envId=2023-11-02)

## 問題

#### 題目大綱

>Given the `root` of a binary tree, return _the number of nodes where the value of the node is equal to the **average** of the values in its **subtree**_.
>**Note:**
>- The **average** of `n` elements is the **sum** of the `n` elements divided by `n` and **rounded down** to the nearest integer.
>- A **subtree** of `root` is a tree consisting of `root` and all of its descendants.
#### 範例

###### 1
**Input:** root = [4,8,5,0,1,null,6]
**Output:** 5
**Explanation:** 
For the node with value 4: The average of its subtree is (4 + 8 + 5 + 0 + 1 + 6) / 6 = 24 / 6 = 4.
For the node with value 5: The average of its subtree is (5 + 6) / 2 = 11 / 2 = 5.
For the node with value 0: The average of its subtree is 0 / 1 = 0.
For the node with value 1: The average of its subtree is 1 / 1 = 1.
For the node with value 6: The average of its subtree is 6 / 1 = 6.

###### 2
**Input:** root = [1]
**Output:** 1
**Explanation:** For the node with value 1: The average of its subtree is 1 / 1 = 1.


## 解法

首先先獲得該點底下有幾個點(包含自己)，並且將底下點的值給總合起來(包含自己)
將該點的總和值去除以底下有幾個點，如果相等則將ans加上一，如果有小數點就無條件捨去

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
    def averageOfSubtree(self, root: Optional[TreeNode]) -> int:
        self.dfs(root)
        return self.ans  

    def dfs(self, currentNode):
        if currentNode is None:
            return 0, 0

        leftTree = self.dfs(currentNode.left)
        rightTree = self.dfs(currentNode.right)
        sumValue = leftTree[0] + rightTree[0] + currentNode.val
        numberNode = leftTree[1] + rightTree[1] + 1

        if (numberNode != 0) and (sumValue // numberNode == currentNode.val):
            self.ans += 1
            
        return sumValue, numberNode
```

#leetcode #tree #dfs 