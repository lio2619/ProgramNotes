## 前因

* 因為在測試的時候需要架設SFTP SERVER，但FileZilla免費版並不支援SFTP
* 在網路上有人推薦SFTPGO，所以這次用這個架設SFTP SERVER

## 下載

* 最簡單的方法：直接去[github](https://github.com/drakkan/sftpgo/releases/tag/v2.6.6)下載對應的版本，下載後啟動exe後一直按下一步就好
* 下載原始碼去執行，但是需要go的環境
* 下載到docker去執行
## 設定

* exe檔安裝完畢後預設會安裝在 C:\\\ProgramData\\\SFTPGo
* 預設的web 網站是 127.0.0.1:8080
* 預設的SFTP SERVER是 127.0.0.1:2022
* 這些都可以在sftpgo.json裡面調整

### sftp server web port 調整

* 可以自己設定要對應的port
```json
"httpd": {
    "bindings": [
      {
        "port": 8080,
        "address": "",
        "enable_web_admin": true,
```
### sftp server port 調整

* 只要把以下的port調整成其他就OK了，記得防火牆需要開
```json
"sftpd": {
    "bindings": [
      {
        "port": 2022,
        "address": "",
        "apply_proxy_config": true
      }
    ],
```

### sftp 相關演算法調整

* 因為 **ssh-rsa**、**ssh-dss** 這兩種演算法不安全，所以在預設的SFTPGO SERVER沒有允許這兩種演算法
* 可以在json裡面加入以下調整就可以使用了，記得每次調整完都要重新啟動SFTPGO
```json
"sftpd": {
    "bindings": [
      {
        "port": 2022,
        "address": "",
        "apply_proxy_config": true
      }
    ],
    "max_auth_tries": 0,
    "host_keys": [],
    "host_certificates": [],
    "host_key_algorithms": [
		"rsa-sha2-256",
		"rsa-sha2-512",
		"ecdsa-sha2-nistp256",
		"ssh-ed25519",
		"ssh-rsa",
		"ssh-dss"
	],
    "kex_algorithms": [],
    "min_dh_group_exchange_key_size": 2048,
    "ciphers": [],
    "macs": [],
    "public_key_algorithms": [
		"ssh-rsa",
		"ssh-dss"
	],
```

```bash
#關閉SFTPGO
net stop sftpgo
#啟動SFTPGO
net start sftpgo
```

## 參考資料

https://github.com/drakkan/sftpgo
[Configuration file - SFTPGo documentation](https://docs.sftpgo.com/devel/config-file/#sshsftp-server)

#SFTP #SFTPSERVER