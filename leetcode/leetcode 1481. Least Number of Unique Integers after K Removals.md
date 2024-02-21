
題目網址：[Least Number of Unique Integers after K Removals - LeetCode](https://leetcode.com/problems/least-number-of-unique-integers-after-k-removals/description/?envType=daily-question&envId=2024-02-20)

## 問題

#### 題目大綱

>Given an array of integers `arr` and an integer `k`. Find the _least number of unique integers_ after   removing **exactly** `k` elements**.**
###### 1
**Input:** arr = [5,5,4], k = 1
**Output:** 1
**Explanation**: Remove the single 4, only 5 is left.
###### 2
**Input:** arr = [4,3,1,1,3,3,2], k = 3
**Output:** 2
**Explanation**: Remove 4, 2 and either one of the two 1s or three 3s. 1 and 3 will be left.
## 解法

這個問題是要刪除 list 裡面 k 個數字，並且將最後list裡面剩下幾個獨特的數字輸出
先將 list 轉成 dict ，並且按照value的最小值做排序，然後依序看 k 值有沒有小於最小值

```python
from collections import Counter
class Solution:
    def findLeastNumOfUniqueInts(self, arr: List[int], k: int) -> int:
        d = sorted(Counter(arr).values())
        fre_sum = len(d)
        for i in d:
            if k < 1:
                break
            if k >= i:
                k -= i
                fre_sum -= 1
            elif k < i:
                break
        return fre_sum
```

#leetcode #hash