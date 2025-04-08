## jenkins

### pipleline
#### 組態設定
* 在這邊設定專案對應的URL以及帳號密碼
![[Pasted image 20250307171057.png]]
* 在這邊設定要從哪個branch建置
![[Pasted image 20250307171128.png]]
* 因為是專案在azure上所以勾選TFS
![[Pasted image 20250307171215.png]]
* 接下來是建置的指令：
1. 將IIS站台暫停
2. 編譯專案並且將它搬到IIS的主機
3. 將IIS站台啟動
- 如果怕有cache的問題可以暫停IIS的應用程式集區
```shell
:: IIS站台暫停
D:
cd D:\PSTools
psexec /accepteula \\192.168.100.XXX powershell -Command "Stop-WebSite -Name 'IISName'"

:: 編譯專案和搬移
dotnet publish --configuration Release --output D:\XXX\Dev C:/ProgramData/Jenkins/.jenkins/workspace/XXX/Web/Web.csproj
robocopy D:\XXX\Dev \\192.168.100.XXX\D$\CFSP /E /COPYALL /NP /NFL /NDL || exit 0

::IIS站台啟動
D:
cd D:\PSTools
psexec /accepteula \\192.168.100.XXX powershell -Command "Start-WebSite -Name 'IISName'"
```

### 放到外網

* 最簡單就用ngrok穿透到外網就好
## azure devops

### 設定 hook步驟
![[Pasted image 20250307173056.png]]
![[Pasted image 20250307173141.png]]
![[Pasted image 20250307173210.png]]
* 這邊輸入ngrok
