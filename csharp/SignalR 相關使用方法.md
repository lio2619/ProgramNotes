## 安裝

* 依照參考資料的方式安裝
* 以下都是在.net 8的環境使用
## 程式碼撰寫

### 後端

#### 先將signalR注入到程式裡面

* /SessionNoticeHub => 代表你將該signalR註冊的url，以後需要呼叫就使用這個url
```csharp
using Lib.Hubs;

var builder = WebApplication.CreateBuilder(args);
// 其餘程式碼
builder.Services.AddSignalR();

var app = builder.Build();
app.UseEndpoints(endpoints =>
{
    endpoints.MapHub<SessionNoticeHub>("/SessionNoticeHub");
});
```
#### 主要程式碼寫法

```csharp
using Microsoft.AspNetCore.SignalR;

namespace Lib.Hubs
{
    public class SessionNoticeHub : Hub
    {
        private static Dictionary<string, string> _userSessions = new Dictionary<string, string>();

        public void RegisterUserSession(string userId)
        {
            var connectionId = Context.ConnectionId;

            // 如果已經有連線存在，表示用戶在其他頁籤登錄，通知用戶登出
            if (_userSessions.ContainsKey(userId))
            {
                var existingConnectionId = _userSessions[userId];
                Clients.Client(existingConnectionId).SendAsync("LogOutForMultipleDevice", userId);
            }
            else
            {
                _userSessions[userId] = connectionId;
            }
        }

        public void OnLogOutForMultipleDevice(string userId)
        {
            // 移除用戶的 session
            if (_userSessions.ContainsKey(userId))
            {
                _userSessions.Remove(userId);
            }
            Clients.Client(Context.ConnectionId).SendAsync("LogOutForMultipleDevice", userId);
        }

        // 當連線被終止時清理 session
        public override async Task OnDisconnectedAsync(Exception? exception)
        {
            var userId = _userSessions.FirstOrDefault(x => x.Value == Context.ConnectionId).Key;
            if (!string.IsNullOrEmpty(userId))
            {
                _userSessions.Remove(userId);
            }
            await base.OnDisconnectedAsync(exception);
        }
    }
}

```
### 前端
#### SignalR的主程式

```javascript

$(document).ready(function () {
    var currentAccountId = localStorage.getItem("AccountId")
    function connect(conn) {
        conn.start()
            .then(() => {
                console.log('opened!' + connection.connectionId)
                connection.invoke("RegisterUserSession", currentAccountId).catch(function (err) {
                    return console.error(err.toString());
                })
            })
            .catch(e => {
                console.error(e.toString());
            })
    }
    let pathBase = getPathBase();
    var connection = new signalR.HubConnectionBuilder()
        .withUrl(pathBase + "/SessionNoticeHub", {
            skipNegotiation: false,
            transport: signalR.HttpTransportType.WebSockets
        })
        .configureLogging(signalR.LogLevel.Error)
        .build();
    connection.serverTimeoutInMilliseconds = getTimeoutMilliseconds(3);
    connection.keepAliveIntervalInMilliseconds = getTimeoutMilliseconds(1);

    connection.on("logOutForMultipleDevice", function (accountId) {
        console.log("logOutForMultipleDevice");
        if (accountId === currentAccountId) {
            logOut();
        }
    });

    connect(connection);
});


function logOut() {
    let pathBase = getPathBase();
    window.location.href = pathBase + '/Login/Logout';
}

function getPathBase() {
    return window.location.origin;
}

function getTimeoutMilliseconds(addSeconds) {
    return (getSessionIdleTimeout() + addSeconds) * 1000 * 60;
}

function getSessionIdleTimeout() {
    return parseInt(30);
}
```

#### 呼叫該script時的程式

* 要記得先呼叫安裝signalr後出現的js檔，不然會出現signalr找不到的問題
* 這邊我是將它放在登入後，不管到哪個網頁都會呼叫一次
```html
<script src="@Url.Content("~/js/signalr/dist/browser/signalr.min.js?v="+DateTime.Now.Ticks)"></script>
<script src="@Url.Content("~/js/SignalRListener.js?v="+DateTime.Now.Ticks)"></script>
```

## 參考資料

https://learn.microsoft.com/zh-tw/aspnet/core/tutorials/signalr?view=aspnetcore-9.0&tabs=visual-studio

#net #javascript 