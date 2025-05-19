## 原因

* 因為要在jenkins上抓取azure裡面的專案進行CICD，所以需要相關的憑證才能連接

## 過程

1. 先在 **azure** 上面按下個人頁面 -> 點擊 **Security** -> 新增 **personal access token** (權限至少要有code (read)) -> 複製他生成的 **toekn**
2. 在 **jenkins** 上面點擊 **Credentials** 選擇 **Global credentials** 新增憑證 -> 如果是https就用 **Username with password**，Username填帳號、password填剛剛複製的token
3. 將下來可以再隨便一個pipeline進行驗證，只要沒有出現錯誤就可以了

## 錯誤解決

```bash
stderr: fatal: Cannot prompt because user interactivity has been disabled.
```
* 如果出現上面的錯誤就代表該帳號沒有權限，去azure上看有沒有設定錯誤

#Jenkin #Azure #CICD 