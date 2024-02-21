
題目網址：[Bitwise AND of Numbers Range - LeetCode](https://leetcode.com/problems/bitwise-and-of-numbers-range/description/?envType=daily-question&envId=2024-02-21)

## 問題

#### 題目大綱

>Given two integers `left` and `right` that represent the range `[left, right]`, return _the bitwise AND of all numbers in this range, inclusive_.
###### 1
**Input:** left = 5, right = 7
**Output:** 4
###### 2
**Input:** left = 0, right = 0
**Output:** 0
###### 3
**Input:** left = 1, right = 2147483647
**Output:** 0
## 解法

這個問題是要將 left ~ right 裡面的值做and後的值輸出出來
如果用迴圈去解的話會出現 time error 的錯誤
所以用位元運算去做解答

```python
class Solution:
    def rangeBitwiseAnd(self, left: int, right: int) -> int:
        shift = 0
        while left < right:
            left >>= 1
            right >>= 1
            shift += 1
        return left << shift
```

以下為步驟
left ： 5 = 0b101  right ： 7 = 0b111
1. left = 0b010    right = 0b011   shift = 1
2. left = 0b001    right = 0b001   shift = 2
3. 出來的答案為 4 = 0b100

#leetcode #位元運算 