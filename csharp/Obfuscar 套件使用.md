## 安裝

* 請在nuget安裝以下套件
![[Pasted image 20241206094936.png]]
## 使用

### 設定檔

* 這個套件是用xml裡面的參數當作設定檔
* Inpath => 要混淆的exe檔案路徑
* OutPath => 混淆過後的exe檔案要儲存的地方
* 如果是要讓某個特定參數不要混淆，可以用skiptype
* - **`skipMethods="true"`**：這個屬性指示 Obfuscator 跳過該類型中的所有方法，這些方法不會被混淆或重命名。
- **`skipFields="true"`**：這個屬性指示 Obfuscator 跳過該類型中的所有字段（成員變數），這些字段不會被混淆或重命名。
- **`skipProperties="true"`**：這個屬性指示 Obfuscator 跳過該類型中的所有屬性，這些屬性不會被混淆或重命名。
- **`skipEvents="true"`**：這個屬性指示 Obfuscator 跳過該類型中的所有事件，這些事件不會被混淆或重命名。
* 更詳細的設定資訊可以看下面的參考資料
```xml
<?xml version='1.0'?>
<Obfuscator>
  <Var name="InPath" value="D:\VSProjects\test\bin\Release" />
  <Var name="OutPath" value="D:\VSProjects\test\bin\Obfuscator" />

  <Module file="$(InPath)\TestProject.exe">
	  <SkipType name="test.Settings" skipMethods="true" skipFields="true" skipProperties="true" skipEvents="true" />
  </Module>
</Obfuscator>
```
### 指令

* 記得要先移動到obfuscar.console儲存的資料夾
```sh
obfuscar.console .\Obfuscar.xml
```
## 證明
* exe執行檔都是用ILSPY反編譯的
### 混淆前
![[Pasted image 20241206095956.png]]
### 混淆後
![[Pasted image 20241206095941.png]]

## 參考資料
https://blog.miniasp.com/post/2023/08/10/Useful-tool-Obfuscar-Open-source-obfuscation-tool-for-NET-assemblies

https://docs.lextudio.com/obfuscar/getting-started/configuration

#net #混淆程式碼