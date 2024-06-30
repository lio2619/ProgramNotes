## 原因

```csharp
string jsonData = @"1&2 (中文)";

WebRequest request = WebRequest.Create("API URL");
request.Method = "POST";
request.ContentType = "application/x-www-form-urlencoded";

 string jsonParameter = JsonConvert.SerializeObject(jsonData);
 string postString = $"data={jsonParameter}";

 using (StreamWriter requestWriter = new StreamWriter(request.GetRequestStream()))
 {
     requestWriter.Write(postString);
 }
```
* 執行以上程式碼後，那支被打的API得到的資訊是 **data=1**
* 會照成這個的原因是因為 **ContentType = "application/x-www-form-urlencoded"**
* 這個格式如果裡面的文字有 **&**、 **=** 就會照成文字被截取的問題
## 解決方式

```csharp
request.ContentType = "application/json";
```
* 將傳遞格式改成這樣就可以正常的傳遞了
## 參考資料
[POST - HTTP | MDN (mozilla.org)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST)

#newwrok #error #postmethod
