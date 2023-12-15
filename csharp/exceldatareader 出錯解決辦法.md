## 出現ExcelDataSetConfiguration不再函示庫裡

* 去nuget安裝ExcelDataReader.DataSet
* [NuGet Gallery | ExcelDataReader.DataSet 3.7.0-develop00385](https://www.nuget.org/packages/ExcelDataReader.DataSet/3.7.0-develop00385)

## 出現System.NotSupportedException: 'No data is available for encoding 1252.

* 先去nuget安裝System.Text.Encoding.CodePages
* [NuGet Gallery | System.Text.Encoding.CodePages 8.0.0](https://www.nuget.org/packages/System.Text.Encoding.CodePages)
* 再去Program.cs或Startup.cs裡面加入以下程式碼
```csharp
System.Text.Encoding.RegisterProvider(System.Text.CodePagesEncodingProvider.Instance);
```
#net #csharp #error