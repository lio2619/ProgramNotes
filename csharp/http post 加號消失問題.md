## 原因

```csharp
string jsonData = @"5y+g";

objRequest = (HttpWebRequest)WebRequest.Create(httpURL);
objRequest.KeepAlive = false;
objRequest.CachePolicy = new HttpRequestCachePolicy(HttpRequestCacheLevel.NoCacheNoStore);
objRequest.Headers["Pragma"] = "no-cache";
objRequest.Headers["Cache-Control"] = "no-cache";
objRequest.Method = "POST";
byte[] bytepost = System.Text.Encoding.UTF8.GetBytes(jsonData);
objRequest.ContentLength = bytepost.Length;
objRequest.ContentType = "application/x-www-form-urlencoded";

 using (StreamWriter requestWriter = new StreamWriter(request.GetRequestStream()))
 {
     requestWriter.Write(jsonData);
 }
```
* 執行以上程式碼後，那支被打的API得到的資訊是 **5y g**
* 會照成這個的原因是因為 **ContentType = "application/x-www-form-urlencoded"**
* 這個格式如果裡面的文字有 **+** 就會被替換成空白
## 解決方式

```csharp
string encodedPostData = HttpUtility.UrlEncode(jsonData, System.Text.Encoding.UTF8);
```
* 先將要傳遞的值轉成html可以正常傳遞的值就可以了
## 參考資料
[POST - HTTP | MDN (mozilla.org)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST)

#netwrok #error #postmethod
