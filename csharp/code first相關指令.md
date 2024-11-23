## 前面步驟

![[Pasted image 20241115092816.png]]
1. 請先安裝上面的套件
2. 將相關程式碼撰寫完畢
## 新增指令

```bash
Add-Migration InitialCreate
```
## 更新資料庫指令

```bash
Update-Database
```
## 獲得更新資料庫的SQL

```bash
Update-Database -Script
# 又或者用以下指令
Script-Migration
```

* 如果需要的是單純一次的SQL，可以執行以下指令
* from後面接之前的MigrationId
* to後面接這次的MigrationId
```bash
Script-Migration -From '20241115010957_InitialCreate' -To '20241120053836_leo'
```

## 參考資料
[新資料庫的程式代碼優先 - EF6 | Microsoft Learn](https://learn.microsoft.com/zh-tw/ef/ef6/modeling/code-first/workflows/new-database)
[套用移轉 - EF Core | Microsoft Learn](https://learn.microsoft.com/zh-tw/ef/core/managing-schemas/migrations/applying?tabs=vs)

#csharp #net #codefirst #SQL