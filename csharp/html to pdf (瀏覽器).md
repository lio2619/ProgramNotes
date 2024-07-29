## 目的

將html轉pdf並且不要使用到其他特殊套件
## 程式碼

```csharp
using System.Diagnostics;

string command = @"-headless -disable-gpu -run-all-compositor-stages-before-draw " +
        @"-print-to-pdf-no-header -no-pdf-header-footer " +
        $@"-print-to-pdf=""C:/User/Desktop/test.pdf"" " +
        $@"""C:/User/Desktop/test.html""";

ProcessStartInfo psi = new ProcessStartInfo();
// edge瀏覽器
psi.FileName = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.ProgramFilesX86), @"Microsoft\Edge\Application\msedge.exe");
// chrome瀏覽器
//psi.FileName = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.ProgramFiles), @"Google\Chrome\Application\chrome.exe");
psi.Arguments = command;
psi.UseShellExecute = false;
psi.CreateNoWindow = true;

using (Process process = new Process())
{
    process.StartInfo = psi;
    process.Start();
    process.WaitForExit();
}
```
## 參考
[List of Chromium Command Line Switches « Peter Beverloo](https://peter.sh/experiments/chromium-command-line-switches/)

#csharp #command