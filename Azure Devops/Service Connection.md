## 原因

* 在azure 上設定CI的時候，會需要 azure 的 service connection才可以做azure上相關的設定，例如以下的功能
	* 自動發PR
	* 自動Publish到指定位置
## 方法

 1. 先建立自己的token：Persional access tokens -> new tokens 設定要改給token的權限(目前最長的使用時間為一年)
 2. project setting -> Service connections -> create -> Azure Repos / Team Foundation Server
## 自動PR

#### 步驟：

1. **前往專案設定**：
    
    - 在 Azure DevOps 中，導航至您的專案。
        
    - 點擊右上角的齒輪圖示，進入「專案設定」（Project Settings）。[IT人助攻+1Stack Overflow+1](https://ithelp.ithome.com.tw/articles/10300591?utm_source=chatgpt.com)[Azure DevOps.tips](https://www.azuredevops.tips/allow-build-agent-to-commit-code/?utm_source=chatgpt.com)
        
2. **選擇儲存庫設定**：
    
    - 在「專案設定」頁面，找到並點擊「儲存庫」（Repositories）。
        
3. **進入安全性設定**：
    
    - 在「儲存庫」頁面，選擇您遇到問題的儲存庫。
        
    - 點擊上方的「安全性」（Security）標籤。[微軟學習](https://learn.microsoft.com/zh-tw/azure/role-based-access-control/permissions/devops?utm_source=chatgpt.com)
        
4. **搜尋並選擇服務帳號**：
    
    - 在「安全性」頁面，使用搜尋框，輸入 `Project Collection Build Service`。
        
    - 選擇顯示的服務帳號，例如 `Project Collection Build Service (YourOrganizationName)`。[IT人助攻](https://ithelp.ithome.com.tw/articles/10300591?utm_source=chatgpt.com)[azuredevopsguide.com+4Stack Overflow+4IT人助攻+4](https://stackoverflow.com/questions/64645816/azuredevops-api-call-for-pull-request-doesnt-work?utm_source=chatgpt.com)[IT人助攻+3Azure DevOps.tips+3Stack Overflow+3](https://www.azuredevops.tips/allow-build-agent-to-commit-code/?utm_source=chatgpt.com)
        
5. **設定權限**：
    
    - 在該服務帳號的權限設定中，找到「拉取請求貢獻」（Pull Request Contribute）權限。
        
    - 將該權限設為「允許」（Allow）。[Stack Overflow](https://stackoverflow.com/questions/64645816/azuredevops-api-call-for-pull-request-doesnt-work?utm_source=chatgpt.com)
        
6. **保存設定**：
    
    - 確保所有變更已保存。
 
 **沒有設定的話會出現以下錯誤**
 ```
 ERROR: TF401027: You need the Git 'PullRequestContribute' permission to perform this action. Details: identity 'Build\62b0e1f2-5457-4789-a7c8-ef0f3c889443', scope 'repository'.
```

## 參考資料
[azure devops token](https://learn.microsoft.com/zh-tw/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops&tabs=Windows)
[service connect 相關資訊](https://learn.microsoft.com/zh-tw/azure/devops/pipelines/library/connect-to-azure?view=azure-devops&WT.mc_id=DT-MVP-4015686#create-an-azure-resource-manager-service-connection-using-workload-identity-federation)
https://learn.microsoft.com/zh-tw/azure/devops/pipelines/build/variables?view=azure-devops&tabs=yaml
[TF401027: You need the Git ‘PullRequestContribute’ permission to perform this action | Fix/Solution – AzureDevOps Guide](https://www.azuredevopsguide.com/tf401027-you-need-the-git-pullrequestcontribute-permission-to-perform-this-action-fix-solution/)
## 內部連接
[[Azure devops 結合 jenkins 進行CI CD]]
[[pipelines 相關設定]]

#Azure #CICD 