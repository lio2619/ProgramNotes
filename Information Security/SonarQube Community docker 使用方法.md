## 使用方式
### 步驟一
* docker pull 
### 步驟二
* 將資料儲存到DB裡面，可以用以下docker compose
```yml
version: "3"
services:
  sonarqube:
    image: sonarqube:community
    depends_on:
      - db
    environment:
      - SONAR_JDBC_URL=jdbc:postgresql://db:5432/sonar
      - SONAR_JDBC_USERNAME=sonartest
      - SONAR_JDBC_PASSWORD=sonartest
    volumes:
      - sonarqube_data:/opt/sonarqube/data
      - sonarqube_extensions:/opt/sonarqube/extensions
      - sonarqube_logs:/opt/sonarqube/logs
    ports:
      - "9000:9000"
  db:
    image: postgres:12
    environment:
      - POSTGRES_USER=sonartest
      - POSTGRES_PASSWORD=sonartest
      - POSTGRES_DB=sonar
    volumes:
      - postgresql:/var/lib/postgresql
      - postgresql_data:/var/lib/postgresql/data
volumes:
  sonarqube_data:
  sonarqube_extensions:
  sonarqube_logs:
  postgresql:
  postgresql_data:
```

* 啟動SonarQude
```bash
docker compose up -d
```
### 步驟三
* 安裝 nuget 套件讓他可以掃描.net 專案
```bash
dotnet tool install --global dotnet-sonarscanner
```
### 步驟四
* 到localhost:9000 登入網站，初始帳密都是：admin
## 參考
https://ithelp.ithome.com.tw/articles/10294624

#docker #SonarQude #白箱掃描 