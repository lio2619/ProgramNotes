## python原程式

```python
import win32gui
import win32con

def SetWindowToTop(hwnd):
    """確定窗口是否最小化，如果最小化就將它放大成原尺寸，不管怎樣都會把窗口置頂"""
    if win32gui.IsIconic(hwnd):
        #最小化
        win32gui.ShowWindow(hwnd, win32con.SW_RESTORE)
    else:
        win32gui.SetForegroundWindow(hwnd)
```

* 在呼叫此副程式時出現以下錯誤

```powershell
pywintypes.error: (0, 'SetForegroundWindow', 'No error message is available')
```

* 這是在呼叫 **win32gui.SetForegroundWindow(hwnd)** 時出現的錯誤，代表找不到要呼叫的視窗
* 在要呼叫前先傳遞鍵盤事件，就可以找到了

## 解決方法

```python
import win32gui
import win32con
import win32com.client

def SetWindowToTop(hwnd):
    """確定窗口是否最小化，如果最小化就將它放大成原尺寸，不管怎樣都會把窗口置頂"""
    if win32gui.IsIconic(hwnd):
        #最小化
        win32gui.ShowWindow(hwnd, win32con.SW_RESTORE)
    else:
	    shell = win32com.client.Dispatch("WScript.Shell") 
	    shell.SendKeys('%')
        win32gui.SetForegroundWindow(hwnd)
```

## 參考

[python - win32gui.SetActiveWindow() ERROR : The specified procedure could not be found - Stack Overflow](https://stackoverflow.com/questions/14295337/win32gui-setactivewindow-error-the-specified-procedure-could-not-be-found)

#error #python 
