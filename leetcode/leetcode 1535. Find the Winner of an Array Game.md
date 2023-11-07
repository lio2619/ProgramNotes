
題目網址：[Find the Winner of an Array Game - LeetCode](https://leetcode.com/problems/find-the-winner-of-an-array-game/description/?envType=daily-question&envId=2023-11-05)

## 問題

#### 題目大綱

>Given an integer array `arr` of **distinct** integers and an integer `k`.

>A game will be played between the first two elements of the array (i.e. `arr[0]` and `arr[1]`). In each round of the game, we compare `arr[0]` with `arr[1]`, the larger integer wins and remains at position `0`, and the smaller integer moves to the end of the array. The game ends when an integer wins `k` consecutive rounds.

>Return _the integer which will win the game_.

>It is **guaranteed** that there will be a winner of the game.

###### 1
**Input:** arr = [2,1,3,5,4,6,7], k = 2
**Output:** 5
**Explanation:** Let's see the rounds of the game:
Round |       arr       | winner | win_count
  1   | [2,1,3,5,4,6,7] | 2      | 1
  2   | [2,3,5,4,6,7,1] | 3      | 1
  3   | [3,5,4,6,7,1,2] | 5      | 1
  4   | [5,4,6,7,1,2,3] | 5      | 2
So we can see that 4 rounds will be played and 5 is the winner because it wins 2 consecutive games.
###### 2
**Input:** arr = [3,2,1], k = 10
**Output:** 3
**Explanation:** 3 will win the first 10 rounds consecutively.
## 解法

這個問題基本上就是邏輯題
如果K值很大的話不能讓他進去迴圈裡面，不然會time error
也不需要將list裡面的element移動位置
```python
def getWinner(self, arr: List[int], k: int) -> int:
        if k == 1:
            return max(arr[0], arr[1])
        if k >= len(arr):
            return max(arr)
            
        win = arr[0]
        ans = 0
        
        for i in range(1, len(arr)):
            if win > arr[i]:
                ans += 1
            else:
                win = arr[i]
                ans = 1
            if ans == k:
                return win
        return win
```

#leetcode #邏輯