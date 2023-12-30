## 建立

```powershell
python -m venv {yourvenvname}
```
* 將大括號內部文字換成你要建立的虛擬環境名字

## 進入虛擬環境

```powershell
{yourvenvname}\Scripts\activate
```
## 離開

```powershell
deactivate
```

## 注意事項

* 如果進入虛擬環境時出現問題，執行以下的程式更改權限
```powershell
Set-ExecutionPolicy Unrestricted -Scope Process
```
[[查看、修改powershell權限]]
## 其他

* 輸出在此環境中有用到的套件
```powershell
python -m pip freeze > requirements.txt
```

* 安裝套件
```powershell
python -m pip install -r requirements.txt
```

## 參考
[12. 虛擬環境與套件 — Python 3.12.1 說明文件](https://docs.python.org/zh-tw/3/tutorial/venv.html)
[python - 'virtualenv' won't activate on Windows - Stack Overflow](https://stackoverflow.com/questions/18713086/virtualenv-wont-activate-on-windows)
[關於執行原則 - PowerShell | Microsoft Learn](https://learn.microsoft.com/zh-tw/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.4)

#虛擬環境 #powershell #python 