題目網址：[Build an Array With Stack Operations - LeetCode](https://leetcode.com/problems/build-an-array-with-stack-operations/description/?envType=daily-question&envId=2023-11-03)

## 問題

#### 題目大綱

>You are given an integer array `target` and an integer `n`.
>You have an empty stack with the two following operations:
>- **`"Push"`**: pushes an integer to the top of the stack.
>- **`"Pop"`**: removes the integer on the top of the stack.
>You also have a stream of the integers in the range `[1, n]`.
>Use the two stack operations to make the numbers in the stack (from the bottom to the top) equal to `target`. You should follow the following rules:
>- If the stream of the integers is not empty, pick the next integer from the stream and push it to the top of the stack.
>- If the stack is not empty, pop the integer at the top of the stack.
>- If, at any moment, the elements in the stack (from the bottom to the top) are equal to `target`, do not read new integers from the stream and do not do more operations on the stack.
>Return _the stack operations needed to build_ `target` following the mentioned rules. If there are multiple valid answers, return **any of them**.
#### 範例

###### 1
**Input:** target = [1,3], n = 3
**Output:** ["Push","Push","Pop","Push"]
**Explanation:** Initially the stack s is empty. The last element is the top of the stack.
Read 1 from the stream and push it to the stack. s = [1].
Read 2 from the stream and push it to the stack. s = [1,2].
Pop the integer on the top of the stack. s = [1].
Read 3 from the stream and push it to the stack. s = [1,3].

###### 2
**Input:** target = [1,3], n = 3
**Output:** ["Push","Push","Pop","Push"]
**Explanation:** Initially the stack s is empty. The last element is the top of the stack.
Read 1 from the stream and push it to the stack. s = [1].
Read 2 from the stream and push it to the stack. s = [1,2].
Pop the integer on the top of the stack. s = [1].
Read 3 from the stream and push it to the stack. s = [1,3].

###### 3
**Input:** target = [1,2], n = 4
**Output:** ["Push","Push"]
**Explanation:** Initially the stack s is empty. The last element is the top of the stack.
Read 1 from the stream and push it to the stack. s = [1].
Read 2 from the stream and push it to the stack. s = [1,2].
Since the stack (from the bottom to the top) is equal to target, we stop the stack operations.
The answers that read integer 3 from the stream are not accepted.
## 解法

```python
class Solution:
	def buildArray(self, target: List[int], n: int) -> List[str]:
        ans = []
        start = 0

        for i in range(1, n + 1):
            if target[start] == i:
                ans.append("Push")
                start += 1
            else:
                ans.extend(("Push", "Pop"))

            if i == target[-1]:
                break
        return ans
```

#leetcode #stack