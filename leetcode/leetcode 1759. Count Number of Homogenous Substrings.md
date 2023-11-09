
題目網址：[LeetCode - The World's Leading Online Programming Learning Platform](https://leetcode.com/problems/count-number-of-homogenous-substrings/submissions/?envType=daily-question&envId=2023-11-09)

## 問題

#### 題目大綱

>Given a string `s`, return _the number of **homogenous** substrings of_ `s`_._ Since the answer may be too large, return it **modulo** `109 + 7`.

>A string is **homogenous** if all the characters of the string are the same.

>A **substring** is a contiguous sequence of characters within a string.

###### 1
**Input:** s = "abbcccaa"
**Output:** 13
**Explanation:** The homogenous substrings are listed as below:
"a"   appears 3 times.
"aa"  appears 1 time.
"b"   appears 2 times.
"bb"  appears 1 time.
"c"   appears 3 times.
"cc"  appears 2 times.
"ccc" appears 1 time.
3 + 1 + 2 + 1 + 3 + 2 + 1 = 13.

###### 2
**Input:** s = "xy"
**Output:** 2
**Explanation:** The homogenous substrings are "x" and "y".

###### 3
**Input:** s = "zzzzz"
**Output:** 15
## 解法

這個問題基本上就是數學題
如果是相同的文字的話，就把右邊的去減掉左邊的再加上1
"aa" => 2 + 1
"aaa" => 3 + 2 + 1
"aabbb" => 2 + 1 + 3 + 2 + 1

```python
def countHomogenous(self, s: str) -> int:
        left = 0
        ans = 0
        for right in range(len(s)):
            if s[left] == s[right]:
                ans += right - left + 1
            else:
                left = right
                ans += 1 
        return ans % (10 ** 9 + 7)
```

#leetcode #邏輯 #math 