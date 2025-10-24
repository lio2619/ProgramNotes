## 原因
* 雖然在專案裡面通常都會將程式碼用 try catch包起來，但是難免會有漏掉或是其他未預期的問題。
* 因此需要在 web 專案啟動時將相關的middleware fillter註冊好
## 處理方式
### filter 紀錄錯誤訊息方式
* 以下為記錄log的filter
```csharp
using Microsoft.AspNetCore.Mvc.Filters;
using NLog;

namespace Lib.Infra.BaseUI.MVC.Attributes
{
    public class ExceptionLoggingFilter : IExceptionFilter
    {
        private static readonly Logger _logger = LogManager.GetLogger("WebLog");

        public void OnException(ExceptionContext context)
        {
            if (context?.Exception == null)
                return;

            var logEvent = new LogEventInfo(LogLevel.Error, _logger.Name, "Unhandled exception occurred");
            logEvent.Message = context.Exception.ToString();
            logEvent.Properties["LogPath"] = Setting.LogPath;
            logEvent.Properties["App"] = "Fatal";
            logEvent.Properties["FileName"] = $"{DateTime.Now.ToString("yyyy-MM-dd")}.log";

            _logger.Log(logEvent);
        }
    }
}
```
* 然後在 **AddControllersWithViews** 裡面註冊他
```csharp
builder.Services.AddControllersWithViews
    (options =>
    {
		options.Filters.Add(typeof(ExceptionLoggingFilter));
    })
    .AddApplicationPart(typeof(BaseController).Assembly)
    .AddDataAnnotationsLocalization()
    .AddViewLocalization()
```
### UseExceptionHandler 紀錄錯誤訊息的方式
* 以下程式碼可以參考
```csharp
app.UseExceptionHandler(errorApp =>
    {
        errorApp.Run(async context =>
        {
            var exceptionFeature = context.Features.Get<IExceptionHandlerPathFeature>();
            var exception = exceptionFeature?.Error;

            // 取得 NLog Logger
            var logger = NLog.LogManager.GetLogger("WebLog");

            // 記錄錯誤（包含路徑與例外訊息）
            var logEvent = new LogEventInfo(LogLevel.Error, logger.Name, "Unhandled exception occurred");
            logEvent.Message = exception.ToString();
            logEvent.Properties["LogPath"] = Setting.LogPath;
            logEvent.Properties["App"] = "Fatal";
            logEvent.Properties["FileName"] = $"{DateTime.Now.ToString("yyyy-MM-dd")}.log";

            logger.Log(logEvent);

            // 固定導向錯誤頁面（不帶錯誤訊息）
            var controller = "Error";
            var action = "Index";
            var redirectUrl = $"/{controller}/{action}";

            context.Response.Redirect(redirectUrl);
        });
    });
```
## 順序
* 在程式碼裡面有多個地方可以進行攔截，例如在 **UseExceptionHandler** 或 **AddControllersWithViews** 裡面的filter。
* 當 MVC 的 controller 出現沒有被抓住的錯誤時，他會先丟到 **AddControllersWithViews** -> **UseExceptionHandler**。
* 不過當 **AddControllersWithViews** 裡面的filter有加入以下的程式碼時，就不會將 **exception** 拋到 **UseExceptionHandler**，也不會傳到後面的filter。
```csharp
public void OnException(ExceptionContext filterContext)
{
	filterContext.ExceptionHandled = true;
	// 後面還有程式碼
}
```
* 在 **AddControllersWithViews** 裡面的filter的順序是從下到上，例如以下的程式碼的順序為：**ExceptionLoggingFilter** -> **ActionLogAttribute**。
```csharp
builder.Services.AddControllersWithViews
    (options =>
    {
        options.Filters.Add<UserAuthorization>();
        // 非開發環境才打開 (因開發環境仍要看詳細錯誤訊息)
        if (builder.Environment.IsDevelopment() == false)
        {
            options.Filters.Add(typeof(ActionLogAttribute));
            //20251016 leo 當出現例外錯誤時記錄錯誤訊息，filter是後面的先執行才會執行前面的
            options.Filters.Add(typeof(ExceptionLoggingFilter));
        }

        options.ModelBindingMessageProvider.SetCustomBinderMessage();
    })
    .AddApplicationPart(typeof(BaseController).Assembly)
    .AddDataAnnotationsLocalization()
    .AddViewLocalization()
```

#net #error 