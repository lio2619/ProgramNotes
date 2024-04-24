## 安裝

* 代表安裝dashboard2.7的版本
```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
```
## dashboard設定檔

* 代表開啟設定檔
```bash
kubectl edit deployment kubernetes-dashboard -n kubernetes-dashboard
```

* 一開始是沒有紅框裡面的東西的，所以它會自動將dashboard登出，鳩算token還沒過期也是一樣
* 加入紅框的文字代表不會自動登出，如果超出token時間會報401
* 注意排版跟參數對不對，如果不對不會讓你修改
![[Pasted image 20240424174301.png]]

## login設定檔

* 這個是可以看到所有東西的使用者設定檔
```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kubernetes-dashboard
```

* 創建登入用token
* 預設為1個小時
```bash
#下面會創建一個3個小時過期的token
kubectl -n kubernetes-dashboard create token admin-user --duration=3h
#下面會創建一個2天過期的token
kubectl -n kubernetes-dashboard create token admin-user --duration=2d
```

## 啟動

* 預設是在localhost:8001
* http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login
```bash
kubectl proxy
```

## 參考資料
1. 安裝
	[Running Kubernetes and the dashboard with Docker Desktop (andrewlock.net)](https://andrewlock.net/running-kubernetes-and-the-dashboard-with-docker-desktop/)
	[dashboard/aio/deploy/recommended.yaml at v2.7.0 · kubernetes/dashboard · GitHub](https://github.com/kubernetes/dashboard/blob/v2.7.0/aio/deploy/recommended.yaml)
2. dashboard設定檔
	[kubernetes dashboard - How can I make the automatic timed logout longer? - Stack Overflow](https://stackoverflow.com/questions/58012223/how-can-i-make-the-automatic-timed-logout-longer)
3. login設定檔
	[dashboard/docs/user/access-control/creating-sample-user.md at master · kubernetes/dashboard · GitHub](https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md)
4. 啟動
	[Running Kubernetes and the dashboard with Docker Desktop (andrewlock.net)](https://andrewlock.net/running-kubernetes-and-the-dashboard-with-docker-desktop/)

#k8s