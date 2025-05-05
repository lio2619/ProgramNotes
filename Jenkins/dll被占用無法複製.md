## 問題

* 在jenkins裡面用以下指令 publish 專案，然後在用robocopy搬移檔案
```shell
dotnet publish --configuration Release --output D:\JCIC\main C:/ProgramData/Jenkins/.jenkins/workspace/109/JCI/Web/Web.csproj

robocopy D:\JCIC\main \\192.168.100.109\D$\JCIC /E /COPYALL /NP /NFL /NDL || exit 0
```

* 有的時候會出現dll被占用所以無法複製的問題
```txt
等候 30 秒... 正在重試... 2025/04/25 17:16:34 錯誤 32 (0x00000020) 正在複製檔案 D:\XXX\main\Common.dll 程序無法存取檔案，因為檔案正由另一個程序使用。
```
## 解決方法

* 可以在jenkins新增以下指令，確保dotnet publish 有正確的釋放資源
* 這是因為他們會共用同一個資料夾，所以才會照成檔案被占用的情況
```shell
dotnet publish --configuration Release --output D:\JCIC\main C:/ProgramData/Jenkins/.jenkins/workspace/109/JCI/Web/Web.csproj

powershell -command "Start-Sleep -Seconds 5"

robocopy D:\JCIC\main \\192.168.100.109\D$\JCIC /E /COPYALL /NP /NFL /NDL || exit 0
```