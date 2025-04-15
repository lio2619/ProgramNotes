## 緣由

* 在工作上總會遇到資料庫格式開varchar(max)的時候，如果傳入格式沒有設定好就會出現問題，這篇是為了解決資料不一致的問題
## 問題

* 當在程式碼寫以下的程式碼，然後傳入DB有時會出現資料截斷的問題
* 這是因為在不同的環境他預設值會不一樣或是DB設定不一致，才導致出現資料截斷的問題
```csharp
using System.Data;
using System.Data.SqlClient;

SqlParameter[] parameters =
                {
                    new SqlParameter("@SubContactId", SqlDbType.VarChar),
                };
```

## 解決方法

* 將程式碼改成以下的寫法就可以解決了
```csharp
using System.Data;
using System.Data.SqlClient;

SqlParameter[] parameters =
                {
                    new SqlParameter("@SubContactId", SqlDbType.VarChar, -1),
                };
```
## 參考資料

https://stackoverflow.com/questions/973260/what-size-do-you-use-for-varcharmax-in-your-parameter-declaration
https://learn.microsoft.com/zh-tw/dotnet/framework/data/adonet/sql/modifying-large-value-max-data

#csharp #SQL