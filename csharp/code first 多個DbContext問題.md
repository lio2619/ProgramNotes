## 問題

* 當在專案裡面有多個DbContext時使用以下指令
```shell
Add-Migration InitialCreate
Update-Database
```
* 會發生以下的Exception
```shell
More than one DbContext was found. Specify which one to use. Use the '-Context' parameter for PowerShell commands and the '--context' parameter for dotnet commands.
```

## 原因

* 這是因為ef core不曉得該用哪個DbContext幫你建立資料庫，因此只要指定好DbContext就可以解決此問題

## 解法

* 到你的專案查看有哪些DbContext或是誰繼承了DbContext，假設有以下程式碼並且你就是要使用此DbContext
```csharp
public class DataDbEntities : DbContext, IDataDbContext
{}
```
* 將code first的指令改成以下就可以正常執行了
```shell
Add-Migration InitialCreate -Context DataDbEntities
Update-Database -Context DataDbEntities
```

#codefirst #net 