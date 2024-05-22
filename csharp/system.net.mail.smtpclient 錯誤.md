# 第一種錯誤

## 報了什麼錯誤
```bash
IOException: 驗證失敗，因為遠端群體已經關閉傳輸資料流。
```
## 為什麼
* 如果有在程式碼內部有開啟SSL驗證，不過驗證方式又和mail server不一樣就會報錯
## 解決方法
* 在程式碼內部加入以下程式就可以正確寄信了
```csharp
System.Net.ServicePointManager.SecurityProtocol = SecurityProtocolType.Ssl3 | SecurityProtocolType.Tls12 | SecurityProtocolType.Tls11 | SecurityProtocolType.Tls;
```
* 因為有些mail server 只支援某種SSL/TLS，所以不能用內建的去執行
# 第二種錯誤
## 報了什麼錯誤
```bash
處理時發生錯誤。 伺服器回應為: 5.7.3 STARTTLS is required to send mail [SI2P153CA0024.APCP153.PROD.OUTLOOK.COM 2024-05-22T01:55:03.712Z 08DC79ECDC21C421]
```
## 為什麼
* 如果在程式碼內部沒有開啟SSL驗證，mail server又需要有SSL驗證就會出現此錯誤
## 解決方法
* 如果原本的程式碼長底下這樣
```csharp
using (SmtpClient client = new SmtpClient(smtpServer, smtpPort))
{
    client.UseDefaultCredentials = useDefaultCredentials;
    //設定帳號密碼，有帳號密碼才執行
    if (!string.IsNullOrEmpty(mailAccount) && !string.IsNullOrEmpty(mailPwd))
    {
        client.Credentials = new NetworkCredential(mailAccount, mailPwd);//寄信帳密
    }
    client.EnableSsl = False;
    client.Send(mms);//寄信
}
```

* 把client.EnableSsl 改成true就可以了
```csharp
using (SmtpClient client = new SmtpClient(smtpServer, smtpPort))
{
    client.UseDefaultCredentials = useDefaultCredentials;
    //設定帳號密碼，有帳號密碼才執行
    if (!string.IsNullOrEmpty(mailAccount) && !string.IsNullOrEmpty(mailPwd))
    {
        client.Credentials = new NetworkCredential(mailAccount, mailPwd);//寄信帳密
    }
    client.EnableSsl = True;
    client.Send(mms);//寄信
}
```

# 參考資料
[security - Default SecurityProtocol in .NET 4.5 - Stack Overflow](https://stackoverflow.com/questions/28286086/default-securityprotocol-in-net-4-5)

#csharp #mail #error