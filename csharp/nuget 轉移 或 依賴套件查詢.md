## 因由

* 在進行專案管控時會需要將所有用到的套件整理起來好做管控。
* 當第三方套件出現弱點時，需要確定該套件是相依在哪個專案底下。

## 方法
### 將所有專案的套件與相依套件列出

```bash
dotnet list package --include-transitive
```

* 在cmd下完上面的指令後會出現類似以下的文字

```txt
專案 'DAL' 有以下套件參考
   [net8.0]:
   最上層套件                                          已要求      已解析
   > Microsoft.EntityFrameworkCore                6.0.11   6.0.11
   > Microsoft.EntityFrameworkCore.Design         6.0.0    6.0.0
   > Microsoft.EntityFrameworkCore.InMemory       6.0.0    6.0.0
   > Microsoft.EntityFrameworkCore.SqlServer      6.0.11   6.0.11
   > System.ServiceModel.Duplex                   6.0.0    6.0.0
   > System.ServiceModel.Federation               6.0.0    6.0.0
   > System.ServiceModel.Http                     6.0.0    6.0.0
   > System.ServiceModel.NetTcp                   6.0.0    6.0.0
   > System.ServiceModel.Security                 6.0.0    6.0.0
   > Z.EntityFramework.Plus.EFCore                6.13.2   6.13.2

   可轉移的套件                                                            已解析
   > AutoMapper                                                      10.1.1
   > AutoMapper.Extensions.Microsoft.DependencyInjection             8.1.1
```
### 將指定的套件有依賴的專案列出

```bash
dotnet nuget why Microsoft.Data.SqlClient
```

* 在why後面接要查詢的套件
* 在cmd下完指令後會輸出類似以下的文字

```
專案 'DAL' 具有下列 'Microsoft.Data.SqlClient' 的相依性關係圖:

  [net8.0]
   │
   ├─ Lib.Interfaces (v1.0.0)
   │  ├─ Common (v1.0.0)
   │  │  └─ ITSLibCore (v6.0.12)
   │  │     └─ Microsoft.EntityFrameworkCore.SqlServer (v6.0.11)
   │  │        └─ Microsoft.Data.SqlClient (v2.1.4)
```

## 環境

* 目前使用的dotnet sdk version = 9.0.203
* 專案是用.net 8開發的

## 參考資料
https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-package-list
https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-nuget-why

#net #csharp #nuget #dotnet

