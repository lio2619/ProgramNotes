## IEnumerable

* 會先將資料都從資料庫拉到記憶體然後再進行filter
![[Pasted image 20240430105730.png]]
## IQueryable

* 會直接在資料庫裡面filter資料，然後再將過濾完的資料拉回記憶體
* 如果是很多資料並且要分頁的情況下，推薦使用IQueryable
![[Pasted image 20240430105741.png]]

## 資料操作

* 如果資料大小比較小推薦使用IEnumerable
* 如果資料大小比較大推薦使用IQueryable
## 參考資料
[Difference between IEnumerable and IList and List, IQueryable? (linkedin.com)](https://www.linkedin.com/pulse/difference-between-ienumerable-ilist-list-iqueryable-pawan-verma)

#csharp #資料結構 #dataStructure