
題目網址：[Find The Original Array of Prefix Xor - LeetCode](https://leetcode.com/problems/find-the-original-array-of-prefix-xor/?envType=daily-question&envId=2023-11-01)

## 問題

#### 題目大綱

>You are given an **integer** array `pref` of size `n`. Find and return _the array_ `arr` _of size_ `n` _that satisfies_:
>- `pref[i] = arr[0] ^ arr[1] ^ ... ^ arr[i]`.
>Note that `^` denotes the **bitwise-xor** operation.
>It can be proven that the answer is **unique**.
#### 範例

###### 1
**Input:** pref = [5,2,0,3,1]
**Output:** [5,7,2,3,2]
**Explanation:** From the array [5,7,2,3,2] we have the following:
- pref[0] = 5.
- pref[1] = 5 ^ 7 = 2.
- pref[2] = 5 ^ 7 ^ 2 = 0.
- pref[3] = 5 ^ 7 ^ 2 ^ 3 = 3.
- pref[4] = 5 ^ 7 ^ 2 ^ 3 ^ 2 = 1.

###### 2
**Input:** pref = [13]
**Output:** [13]
**Explanation:** We have pref[0] = arr[0] = 13.


## 解法

這個問題主要是考XOR的交換率
例如：5 ^ 7 = 2 那 2 ^ 7 = 5
知道這點之後就把東西邏輯寫進去程式裡就好

```python
def findArray(self, pref: List[int]) -> List[int]:
	ans = [pref[0]]
	for i in range(1, len(pref)):
		ans.append(pref[i - 1] ^ pref[i])
	return ans
```

#leetcode #位元運算 #XOR