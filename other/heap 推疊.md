## 介紹

heap是一個二元樹

## 程式範例
#### python

python的heapq這個model是min heap 也就是說他pop出去的會是最小值
```python
import heapq
array = [2, 7, 4, 1]
heapq.heapify(array)        #這一步是為了讓這個list符合heap的條件
heapq.heappop(array)        #這一步會將最小值取出來
heapq.heappush(array, 10)   #這一步會將10這個元素放進去，一樣會依照heap的規則
```
## 範例
[[leetcode 1845. Seat Reservation Manager]]

## 參考
[[Day 24] 從零開始學Python - 資料結構模組heapq：除了前幾名以外，在座的各位都是垃圾 - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天 (ithome.com.tw)](https://ithelp.ithome.com.tw/articles/10247299)
[heapq --- 堆積佇列 (heap queue) 演算法 — Python 3.12.0 說明文件](https://docs.python.org/zh-tw/3/library/heapq.html)

#heap