
## 為什麼

1. 如果網路不好會發生time out (http error code 502)的錯誤
2. 如果從資料庫那邊撈很久也會出現502的錯誤

## 如何操作

### url rewrite 機器

* 點選左側網站，會看到底下的畫面，按下紅框處的選項
![[Pasted image 20240424140331.png]]

* 點進來後按下右側紅框
![[Pasted image 20240424140414.png]]

* 在紅框裡面輸入你要設定的time out 秒數
![[Pasted image 20240424140458.png]]
### 導向的機器

* 點選站台並且按下右邊紅框
![[Pasted image 20240424141137.png]]

* 在紅框裡面調整time out的時間
![[Pasted image 20240424141222.png]]

### 程式的web.config

* 修改紅框處的設定 **單位是秒**
![[Pasted image 20240424140911.png]]

## 參考資料
[node.js - IIS URL REWRITE TIMEOUT IN 1 mins - Stack Overflow](https://stackoverflow.com/questions/71939514/iis-url-rewrite-timeout-in-1-mins)

#iis #timeout #csharp #net 