
題目網址：[Power of Two - LeetCode](https://leetcode.com/problems/power-of-two/description/?envType=daily-question&envId=2024-02-19)

## 問題

#### 題目大綱

>Given an integer `n`, return _`true` if it is a power of two. Otherwise, return `false`_.
   An integer `n` is a power of two, if there exists an integer `x` such that `n == 2x`.
###### 1
**Input:** n = 1
**Output:** true
**Explanation:** 2^0 = 1
###### 2
**Input:** n = 16
**Output:** true
**Explanation:** 2^4 = 16
###### 3
**Input:** n = 3
**Output:** false
## 解法

這個問題是要問傳入的n是否為2的指數

```bash
1 = 0000 0001   0 = 0000 0000
2 = 0000 0010   1 = 0000 0001
4 = 0000 0100   3 = 0000 0011
```

可以透過上面的二進位發現，n and (n - 1) 如果n為2的指數的話就會等於0
藉由這個結論可以推導出下面的程式

```python
class Solution:
    def isPowerOfTwo(self, n: int) -> bool:
        if n < 1:
            return False
        return n & (n - 1) == 0
```

#leetcode #位元運算 