## 為什麼
* 因為迴圈執行到一半，就將list裡面的元素給刪除
## 方法
* 會出現問題的寫法，問題點是remove那一行
```csharp
List<string> fileList = new List<string>(File.ReadAllLines(filePath)); 
foreach (var file in fileList) 
{ 
	string[] fileReadLine = file.Split('|'); 
	if (File.Exists(fileReadLine[0])) 
	{ 
		DateTime lastWriteTime = File.GetLastWriteTime(fileReadLine[0]); 
		DateTime FTPFileLastWriteTime = DateTime.Parse(fileReadLine[1]); 
		// 如果本機檔案的修改時間比FTP上面的時間還晚就不要更新 
		if (lastWriteTime >= FTPFileLastWriteTime) 
		{ 
			fileList.Remove(file); 
		}
	} 
}
```

* 解決方法
```csharp
List<string> fileList = new List<string>(File.ReadAllLines(filePath));
fileList.RemoveAll(file =>
{
    string[] fileReadLine = file.Split('|');
    if (File.Exists(fileReadLine[0]))
    {
        DateTime lastWriteTime = File.GetLastWriteTime(fileReadLine[0]);
        DateTime FTPFileLastWriteTime = DateTime.Parse(fileReadLine[1]);
        // 如果本機檔案的修改時間比FTP上面的時間還晚就不要更新
        return lastWriteTime >= FTPFileLastWriteTime;
    }
    return false;
});
```
* RemoveAll如果裡面回傳true就會將那一個元素刪掉，如果回傳false就不刪

#csharp #error 