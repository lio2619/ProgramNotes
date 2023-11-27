# 在做升級版本前一定要記得備份
## 安裝升級套件

### 安裝套件 
* 開啟visual studio後在上面的選項裡面選衍生模組 => 管理衍生模組
* 安裝.net upgrade assistant那個模組
![[螢幕擷取畫面 2023-11-27 221134.png]]
* 安裝完後將visual studio關閉，系統會跑出安裝視窗，照者它跑出的視窗執行就可以安裝成功了

## 升級專案

### 開啟專案
* 在專案的地方案右鍵，會跑出以下資料，按下upgrade

![[螢幕擷取畫面 2023-11-27 221435.png]]
* 會跑出以下的東西，選擇第一個並且在之後的頁面選擇要升級的版本就可以了
![[螢幕擷取畫面 2023-11-27 221507.png]]

## 有可能出現的問題

* **填滿綠色核取記號**：成品已升級並成功完成。
- **未填滿綠色核取記號**：此工具找不到要升級之成品的任何專案。
- **黃色警告符號**：成品已升級，但您應該考慮重要資訊。
- **紅色 _X_**：成品已升級，但升級失敗。
## 參考資料

[如何安裝 .NET 升級小幫手 - .NET Core | Microsoft Learn](https://learn.microsoft.com/zh-tw/dotnet/core/porting/upgrade-assistant-install#install-the-visual-studio-extension)
[.NET 升級小幫手的概觀 - .NET Core | Microsoft Learn](https://learn.microsoft.com/zh-tw/dotnet/core/porting/upgrade-assistant-overview)

#net #升級版本