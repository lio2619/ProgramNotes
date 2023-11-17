
題目網址：[Find Unique Binary String - LeetCode](https://leetcode.com/problems/find-unique-binary-string/description/?envType=daily-question&envId=2023-11-16)
## 問題

#### 題目大綱

>Given an array of strings `nums` containing `n` **unique** binary strings each of length `n`, return _a binary string of length_ `n` _that **does not appear** in_ `nums`_. If there are multiple answers, you may return **any** of them_.

###### 1
**Input:** nums = ["01","10"]
**Output:** "11"
**Explanation:** "11" does not appear in nums. "00" would also be correct.
###### 2
**Input:** nums = ["00","01"]
**Output:** "11"
**Explanation:** "11" does not appear in nums. "10" would also be correct.
###### 3
**Input:** nums = ["111","011","001"]
**Output:** "101"
**Explanation:** "101" does not appear in nums. "000", "010", "100", and "110" would also be correct.
## 解法

這個問題是要找出不會nums裡面的2進位數字
所以只要把nums裡面每一個位元的東西取相反就好

```python
def findDifferentBinaryString(self, nums: List[str]) -> str:
        ans = ""
        for i in range(len(nums)):
            if nums[i][i] == "0":
                ans += "1"
            else:
                ans += "0"
        return ans
```

#leetcode #位元運算 