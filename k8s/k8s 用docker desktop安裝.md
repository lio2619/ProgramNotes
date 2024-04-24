## docker desktop安裝

* 請去[Get Docker | Docker Docs](https://docs.docker.com/get-docker/?_gl=1*1uc3d0v*_ga*MTMxMDc3MzIwOC4xNzEzOTQwNjQ0*_ga_XJWPQMJYHQ*MTcxMzk0MDY0NC4xLjEuMTcxMzk0MDY1NC41MC4wLjA.)安裝
* 一直按下一步就好
* 最後因為要幫你啟動hyper v，所以會需要重新開機

## k8s安裝

### 啟動docker desktop，並且進入設定

* 按下上面紅框處的齒輪，進入進定頁面
![[Pasted image 20240424144045.png]]

### 安裝k8s

1. 先按下紅框處的按鈕
2. 再將綠框處的勾勾勾選起來
3. 最後按下籃框處的紅紐確定安裝
![[Pasted image 20240424144316.png]]

## 確定k8s安裝成功

### GUI介面確定
* 紅框處的ks8 icon是綠色的就確定有安裝成功
![[Pasted image 20240424144823.png]]

### CLI介面確定
* 也可以在CLI介面下以下的指令，如果跑出下面的圖片也代表安裝成功
```bash
kubectl version
```
![[Pasted image 20240424144955.png]]

#k8s #docker