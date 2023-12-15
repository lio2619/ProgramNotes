## 前置流程
* 將資料庫與專案都建立好
* 安裝[NuGet Gallery | dotnet-ef 7.0.14](https://www.nuget.org/packages/dotnet-ef/7.0.14#versions-body-tab)
* 安裝[NuGet Gallery | Pomelo.EntityFrameworkCore.MySql 7.0.0](https://www.nuget.org/packages/Pomelo.EntityFrameworkCore.MySql)
* 安裝[NuGet Gallery | Microsoft.EntityFrameworkCore.Design 8.0.0](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Design/)
* 去專案的csprof檔裡面在PropertyGroup加入以下程式碼，
```csproj
<GenerateRuntimeConfigurationFiles>True</GenerateRuntimeConfigurationFiles>
```
## 指令

```powershell
dotnet ef dbcontext scaffold "server=localhost;Port=3306;Database=yourdatabase; User=yourusername;Password=yourpassword;" "Pomelo.EntityFrameworkCore.MySql" -o ./Models -c YourDbContext -f
```
* 將 **yourdatabase** 改成資料庫的名稱
* 將 **yourusername** 改成資料庫使用者的名稱
* 將 **youruserpassword** 改成資料庫使用者的密碼
* -o 後面接要輸出程式的位置
* -c 後面接context要叫甚麼名字
* -f 會把輸出的東西覆蓋掉

## 參考資料
[[Day05] Entity Framework Core與DB First - 我與 ASP.NET Core 3 的 30天 - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天 (ithome.com.tw)](https://ithelp.ithome.com.tw/articles/10240045)
[c# - Your startup project doesn't reference Microsoft.EntityFrameworkCore.Design - Stack Overflow](https://stackoverflow.com/questions/52536588/your-startup-project-doesnt-reference-microsoft-entityframeworkcore-design)
#net #db