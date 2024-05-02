
## 為什麼要用jwt token

1. jwt token不會儲存在資料庫裡面，也就是說會減輕資料庫的負擔
2. 支援跨域訪問 ( CORS )
## jwt token
### 登入後從後端丟給前端
1. 通常前端會將帳號、密碼丟給後端
2. 後端會回傳一個jwt token給前端
3. 前端可以將jwt token儲存到 **local storage** 或 **session storage** 裡面
```json
{ 
"jwtToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkphbWVzIExvbmcgVGVzdCIsImlhdCI6MTUxNjIzOTAyMn0.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c" }
```
### 前端call api將jwt token給後端
1. 會將jwt token放在api 的 header上面
2. 不要放在body裡面，比較容易被竊取
```javascript
fetch('/api/data', { 
		method: 'GET', 
		headers: { 
		  'Authorization': 'Bearer ' + jwtToken 
		} 
		}) 
.then(response => { 
		// 處理回傳資料 
		});
```
### 需要refresh jwt token時
1. 會在原本的jwt token失效前回傳新的jwt token給前端
2. 其他的跟登入的第二項之後相同

#jwt #token #驗證