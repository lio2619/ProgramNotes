
題目網址：[1921. Eliminate Maximum Number of Monsters](https://leetcode.com/problems/eliminate-maximum-number-of-monsters/)

## 問題

#### 題目大綱

>You are playing a video game where you are defending your city from a group of `n` monsters. You are given a **0-indexed** integer array `dist` of size `n`, where `dist[i]` is the **initial distance** in kilometers of the `ith` monster from the city.

>The monsters walk toward the city at a **constant** speed. The speed of each monster is given to you in an integer array `speed` of size `n`, where `speed[i]` is the speed of the `ith` monster in kilometers per minute.

>You have a weapon that, once fully charged, can eliminate a **single** monster. However, the weapon takes **one minute** to charge. The weapon is fully charged at the very start.

>You lose when any monster reaches your city. If a monster reaches the city at the exact moment the weapon is fully charged, it counts as a **loss**, and the game ends before you can use your weapon.

>Return _the **maximum** number of monsters that you can eliminate before you lose, or_ `n` _if you can eliminate all the monsters before they reach the city._

###### 1
**Input:** dist = [1,3,4], speed = [1,1,1]
**Output:** 3
**Explanation:**
In the beginning, the distances of the monsters are [1,3,4]. You eliminate the first monster.
After a minute, the distances of the monsters are [X,2,3]. You eliminate the second monster.
After a minute, the distances of the monsters are [X,X,2]. You eliminate the thrid monster.
All 3 monsters can be eliminated.
###### 2
**Input:** dist = [1,1,2,3], speed = [1,1,1,1]
**Output:** 1
**Explanation:**
In the beginning, the distances of the monsters are [1,1,2,3]. You eliminate the first monster.
After a minute, the distances of the monsters are [X,0,1,2], so you lose.
You can only eliminate 1 monster.

###### 3
**Input:** dist = [3,2,4], speed = [5,3,2]
**Output:** 1
**Explanation:**
In the beginning, the distances of the monsters are [3,2,4]. You eliminate the first monster.
After a minute, the distances of the monsters are [X,0,2], so you lose.
You can only eliminate 1 monster.
## 解法

這個問題基本上就是邏輯題
先算出每個怪獸的平均移動速度，並且排序後就能知道哪些怪獸是需要先殺掉的
如果怪物的平均速度比裝填速度快則回傳殺到第幾個怪獸

```python
def eliminateMaximum(self, dist: List[int], speed: List[int]) -> int:
	averageSpeed = [dist[i] / speed[i] for i in range(len(dist))]
	averageSpeed.sort()

	for i in range(len(averageSpeed)):
		if averageSpeed[i] <= i:
			return i
	return len(dist)
```


#leetcode #邏輯