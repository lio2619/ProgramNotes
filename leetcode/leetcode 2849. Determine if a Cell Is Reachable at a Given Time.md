
題目網址：[Determine if a Cell Is Reachable at a Given Time - LeetCode](https://leetcode.com/problems/determine-if-a-cell-is-reachable-at-a-given-time/description/?envType=daily-question&envId=2023-11-08)

## 問題

#### 題目大綱

>You are given four integers `sx`, `sy`, `fx`, `fy`, and a **non-negative** integer `t`.

>In an infinite 2D grid, you start at the cell `(sx, sy)`. Each second, you **must** move to any of its adjacent cells.

>Return `true` _if you can reach cell_ `(fx, fy)` _after **exactly**_ `t` **_seconds_**, _or_ `false` _otherwise_.

>A cell's **adjacent cells** are the 8 cells around it that share at least one corner with it. You can visit the same cell several times.

###### 1
**Input:** sx = 2, sy = 4, fx = 7, fy = 7, t = 6
**Output:** true
**Explanation:** Starting at cell (2, 4), we can reach cell (7, 7) in exactly 6 seconds by going through the cells depicted in the picture above.
###### 2
**Input:** sx = 3, sy = 1, fx = 7, fy = 3, t = 3
**Output:** false
**Explanation:** Starting at cell (3, 1), it takes at least 4 seconds to reach cell (7, 3) by going through the cells depicted in the picture above. Hence, we cannot reach cell (7, 3) at the third second.
## 解法

這個問題基本上就是數學題
它可以往8方向移動(左、右、上、下、左上、左下、右上、右下)，每一秒只能移動一次
它最大的移動距離就是用斜的方式移動，所以只需要將起始地跟結束地的座標相減，不要超過t就好
需要注意的是如果t = 1它沒有辦法回到起始地

```python
def isReachableAtTime(self, sx: int, sy: int, fx: int, fy: int, t: int) -> bool:
        if sx == fx and sy == fy:
            return t > 1 or t == 0
        x = abs(sx - fx)
        y = abs(sy - fy)  

        if x > t or y > t:
            return False
        return True
```

#leetcode #邏輯 #math