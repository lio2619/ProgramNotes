## 原因

* 當想要確保推到main分支的code是可以正常建置的就可以使用該pipeline，並且也可以自動建立PR
* 如果可以的話用shell用bash或powershell，vmImage如果是windows shell預設為cmd，但是cmd有的時候會有奇怪的問題
## 方法

```yaml
# 當 push 至 dev 分支時觸發此 Pipeline
trigger:
  - dev

pool:
  vmImage: 'windows-latest'

variables:
  project: 'Web/Web.csproj'
  buildConfiguration: 'Release'

steps:
# 1. 使用 .NET 8 SDK
- task: UseDotNet@2
  inputs:
    packageType: 'sdk'
    version: '8.x'

# 2. 還原 NuGet 相依性
- script: dotnet restore
  displayName: 'Restore NuGet Packages'

# 3. 編譯專案
- script: dotnet build --configuration $(buildConfiguration)
  displayName: 'Build .NET 8 Project'

# 4. 執行單元測試（若有的話）
#- script: dotnet test --configuration $(buildConfiguration)
#  displayName: 'Run Unit Tests'

# 5. 建置成功後，自動建立 Pull Request (僅在前面步驟成功時執行)
- bash: |
    az extension add --name azure-devops

    az devops configure --defaults organization='$(System.TeamFoundationCollectionUri)' project='$(System.TeamProject)'
    
    echo "Organization: $(System.TeamFoundationCollectionUri)"
    echo "Project: $(System.TeamProject)"
    echo "Repository: $(Build.Repository.Name)"
    echo "Source Branch: $(Build.SourceBranchName)"
    echo "Target Branch: main"

    # 建立 PR，此處從來源分支 (例如 dev) 指定合併到 main
    az repos pr create \
      --repository '$(Build.Repository.Name)' \
      --source-branch '$(Build.SourceBranchName)' \
      --target-branch main \
      --title "自動 PR: $(Build.SourceBranchName) -> main" \
      --description "此 PR 由 Pipeline 自動建立，請進行 Code Review"
  displayName: 'Create Pull Request'
  condition: succeeded()  # 僅在前面工作全部成功時執行
  env:
    # 使用系統的存取權杖來驗證 API 呼叫
    AZURE_DEVOPS_EXT_PAT: $(System.AccessToken)

# 5. 當前面步驟皆成功時，直接自動合併 dev 到 main
# - script: |
#     # 設定 Git 使用者資訊（請根據需要調整）
#     git config user.email $("Build.RequestFotEmail")
#     git config --global user.name "Build Bot"
    
#     # 取得最新的遠端更新
#     git fetch origin
    
#     # 切換到 main 分支並更新
#     git checkout main
#     git pull origin main

#     # 合併來自當前分支 (dev) 的變更，並以 no-fast-forward 模式合併
#     git merge origin/dev --no-ff -m "自動合併 dev 分支到 main"
    
#     # 推送合併後的 main 分支到遠端庫
#     git push origin main
#   displayName: 'Auto Merge dev into main'
#   condition: succeeded()
#   env:
#     # 允許腳本存取 OAuth Token，需在 Pipeline 設定中勾選「Allow scripts to access the OAuth token」
#     SYSTEM_ACCESSTOKEN: $(System.AccessToken)
```
## 參考資料


## 內部連接
[[Service Connection]]
[[Azure devops 結合 jenkins 進行CI CD]]

#Azure #CICD 