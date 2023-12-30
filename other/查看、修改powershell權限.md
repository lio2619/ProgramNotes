## 獲取目前的權限

```powershell
 Get-ExecutionPolicy
```
* Restricted 
	* Windows 用戶端電腦的預設執行原則。
	- 允許個別命令，但不允許腳本。
	- 防止執行所有腳本檔案，包括格式化和組態檔 （ `.ps1xml` ）、模組腳本檔案 （ `.psm1` ） 和 PowerShell 設定檔 （ `.ps1` ）。 
	
* Unrestricted 
	* 非 Windows 電腦的預設執行原則，無法變更。
	- 未簽署的腳本可以執行。 執行惡意腳本的風險。
	- 在執行不是來自近端內部網路區域的腳本和組態檔之前，先警告使用者。
## 更改權限

```powershell
 Set-ExecutionPolicy Unrestricted -Scope Process
```
- **Set-ExecutionPolicy** 是一個cmdlet，用於更改PowerShell的執行策略
- **Unrestricted** 是一種執行策略，表示可以運行任何腳本，不受任何限制
- **-Scope Process** 表示這個更改只適用於當前的PowerShell進程
- **-Scope LocalMachine** 表示是全域修改，不過需要 **管理員權限** 才能進行
## 參考
[關於執行原則 - PowerShell | Microsoft Learn](https://learn.microsoft.com/zh-tw/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.4)

[[透過venv建立虛擬環境]]

#powershell 