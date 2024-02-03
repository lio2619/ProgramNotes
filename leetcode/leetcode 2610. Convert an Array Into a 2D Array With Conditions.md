
題目網址：[Convert an Array Into a 2D Array With Conditions - LeetCode](https://leetcode.com/problems/convert-an-array-into-a-2d-array-with-conditions/description/?envType=daily-question&envId=2024-01-09)
## 問題

#### 題目大綱

>You are given an integer array `nums`. You need to create a 2D array from `nums` satisfying the following conditions:

- The 2D array should contain **only** the elements of the array `nums`.
- Each row in the 2D array contains **distinct** integers.
- The number of rows in the 2D array should be **minimal**.

> Return _the resulting array_. If there are multiple answers, return any of them.
> **Note** that the 2D array can have a different number of elements on each row.

###### 1
**Input:** nums = [1,3,4,1,2,3,1]
**Output:** [ [1,3,4,2],[1,3],[1] ]
**Explanation:** We can create a 2D array that contains the following rows:
- 1,3,4,2
- 1,3
- 1
All elements of nums were used, and each row of the 2D array contains distinct integers, so it is a valid answer.
It can be shown that we cannot have less than 3 rows in a valid array.
###### 2
**Input:** nums = [1,2,3,4]
**Output:** [ [4,3,2,1] ]
**Explanation:** All elements of the array are distinct, so we can keep all of them in the first row of the 2D array.
## 解法

這個問題是要將原本的陣列拆解成二維陣列，並且陣列之間的數字不能相同

```python
class Solution:
    def findMatrix(self, nums: List[int]) -> List[List[int]]:
        ans = []

        while nums:
            temp = []
            for num in nums:
                if num not in temp:
                    temp.append(num)
            for i in temp:
                nums.remove(i)
            ans.append(temp)
        return ans
```

## 另一種解法

```python
def findMatrix(self, nums: List[int]) -> List[List[int]]:
	# Dictionary to keep track of the count of each number in nums
	count_nums = {}

	# The resulting 2D array
	ans = []

	# Iterate through each number in the nums array
	for num in nums:
		# If the number is not in count_nums, initialize it with 0
		if num not in count_nums:
			count_nums[num] = 0

		# Get the current count of num, which will be the index in ans
		idx = count_nums[num]

		# If idx is equal to the length of ans, it means we need a new row
		if idx == len(ans):
			ans.append([])

		# Add the number to the row in ans at index idx
		ans[idx].append(num)

		# Increment the count of num in count_nums
		count_nums[num] += 1
	return ans
```
* [Beats 99.52% of users with Python3. Easy solution with comments - Convert an Array Into a 2D Array With Conditions - LeetCode](https://leetcode.com/problems/convert-an-array-into-a-2d-array-with-conditions/solutions/4489651/beats-99-52-of-users-with-python3-easy-solution-with-comments/?envType=daily-question&envId=2024-01-09)


#leetcode #array #hash 