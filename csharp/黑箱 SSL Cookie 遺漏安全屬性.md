## 問題
* 因Set-Cookie: .AspNetCore.Antiforgery裡面沒有設定 **secure** 所以被掃出這個問題

## 解決方式
* 目前的專案為.net 8 web MVC
```csharp
builder.Services.AddSingleton<ConditionalIgnoreAntiforgeryTokenAttribute>();

builder.Services.AddSession(options =>
{
    options.IdleTimeout = TimeSpan.FromMinutes(30);
    options.Cookie.SecurePolicy = builder.Environment.IsProduction() ? CookieSecurePolicy.Always : CookieSecurePolicy.SameAsRequest;
    options.Cookie.SameSite = SameSiteMode.Lax;
    options.Cookie.IsEssential = true;
});

builder.Services.AddAntiforgery(options =>
{
    options.Cookie.SecurePolicy = builder.Environment.IsProduction() ? CookieSecurePolicy.Always : CookieSecurePolicy.SameAsRequest;
    options.Cookie.SameSite = SameSiteMode.Lax;
    options.Cookie.IsEssential = true;
});
```
* 然後自己新增一個attribute，要記的跟上面DI進去的attribute名稱一樣
```csharp
using Microsoft.AspNetCore.Hosting;
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Mvc.Filters;
using Microsoft.Extensions.Hosting;
using System;
using System.Linq;

// 20251110 leo 新增當開發環境時跳過Antiforgery驗證

namespace Common.Attributes
{
    public class ConditionalIgnoreAntiforgeryTokenAttribute : Attribute, IAuthorizationFilter
    {
        private readonly IWebHostEnvironment _env;

        public ConditionalIgnoreAntiforgeryTokenAttribute(IWebHostEnvironment env)
        {
            _env = env;
        }

        public void OnAuthorization(AuthorizationFilterContext context)
        {
            // 僅開發 / 測試環境跳過 Antiforgery
            if (_env.IsDevelopment() || _env.IsEnvironment("Test"))
            {
                var antiforgeryFilter = context.Filters
                    .OfType<AutoValidateAntiforgeryTokenAttribute>()
                    .FirstOrDefault();
                if (antiforgeryFilter != null)
                {
                    context.Filters.Remove(antiforgeryFilter);
                }
            }
        }
    }
}
```
* 接下來再登入的controller加入上面的attribute，以防開發環境跟正式環境連線的方式不同
```csharp
/// <summary>
/// 登入.
/// </summary>
/// <param name="model">使用者登入資料</param>
/// <returns>使用者登入結果</returns>
[AllowAnonymous]
[HttpPost]
[ServiceFilter(typeof(ConditionalIgnoreAntiforgeryTokenAttribute))]
public IActionResult Login(LoginModel model)
{
}
```
### 注意事項

* 開發、正式環境注意事項
	- 開發環境需要下使用以下指令
	    - dotnet publish --configuration Release -p:EnvironmentName=Development --output D:\\test D:/VSProjects/CoreWeb.csproj
	    - 又或者在pubxml設定檔裡面加入以下文字
		```
		<EnvironmentName>Development</EnvironmentName>
		```
	- 正式環境需要下使用以下指令
	    - dotnet publish --configuration Release -p:EnvironmentName=Production --output D:\\test D:/VSProjects/CoreWeb.csproj
	    - 又或者在pubxml設定檔裡面加入以下文字
		```
		<EnvironmentName>Production</EnvironmentName>
		```

* 這些指令的操作只是讓 web.config 裡面多一個 **ASPNETCORE_ENVIRONMENT** 的變數，好讓專案去判斷目前是在什麼環境
* IsProduction() = **ASPNETCORE_ENVIRONMENT** = Production
* IsDevelopment() = **ASPNETCORE_ENVIRONMENT** = Development
* 
## 參考資料
[如何透過 dotnet publish 調整 ASP․NET Core 部署到 IIS 的 Web.config 內容 | The Will Will Web](https://blog.miniasp.com/post/2023/03/30/How-to-set-environment-name-for-webconfig-when-run-dotnet-publish)
[CookieSecurePolicy 列舉 (Microsoft.AspNetCore.Http) | Microsoft Learn](https://learn.microsoft.com/zh-tw/dotnet/api/microsoft.aspnetcore.http.cookiesecurepolicy?view=aspnetcore-8.0)
[SameSiteMode 列舉 (System.Web) | Microsoft Learn](https://learn.microsoft.com/zh-tw/dotnet/api/system.web.samesitemode?view=netframework-4.8.1)

#net #黑箱 #SSL #web設定檔