## 原因
* 如果沒有自架MCP SERVER的話，當出現錯誤有的時候gemini無法準確的資到錯誤訊息是什麼，以及為了減省將錯誤訊息貼給AI的時間。

## MCP SERVER 程式碼
* 要先安裝 **ModelContextProtocol** 、**ModelContextProtocol.AspNetCore**
* 目前自架的專案環境為 .net 8
```csharp
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;
using ModelContextProtocol.Server;

namespace GeminiCliMCPServer
{
    class Program
    {
        static async Task Main(string[] args)
        {
            var builder = Host.CreateDefaultBuilder(args);

            builder.ConfigureLogging(logging =>
            {
                logging.AddConsole(options =>
                {
                    options.LogToStandardErrorThreshold = LogLevel.Trace;
                });
            });

            builder.ConfigureServices(services =>
            {
                services.AddMcpServer()
                        .WithHttpTransport()
                        .WithStdioServerTransport()
                        .WithToolsFromAssembly(); // 掃描工具
            });

            var host = builder.Build();
            await host.RunAsync();
        }
    }

    [McpServerToolType]
    public static class Tools
    {
        [McpServerTool(Name = "echo"), System.ComponentModel.Description("Echo back the message")]
        public static string Echo(string message)
        {
            return $"Echo: {message}";
        }

        [McpServerTool(Name = "getLastError"), System.ComponentModel.Description("Get last error from specified log file")]
        public static string GetLastError(string logFile)
        {
            if (!File.Exists(logFile))
                return $"No log found at {logFile}.";

            var lines = File.ReadAllLines(logFile);
            return lines.Length > 0 ? lines[^1] : "No error recorded.";
        }

        [McpServerTool(Name = "getLastErrorFromDirectory"), System.ComponentModel.Description("Get last error from latest modified log in directory")]
        public static string GetLastErrorFromDirectory(string logDir)
        {
            if (!Directory.Exists(logDir))
                return $"Directory not found: {logDir}";

            var logFiles = Directory.GetFiles(logDir, "*.log");
            if (logFiles.Length == 0)
                return "No log files found.";

            var latestFile = logFiles.OrderByDescending(f => File.GetLastWriteTime(f)).First();
            var lines = File.ReadAllLines(latestFile);
            return lines.Length > 0 ? lines[^1] : "No error recorded.";
        }

        [McpServerTool(Name = "getAllLastErrors"), System.ComponentModel.Description("Get last errors from all logs in directory")]
        public static string[] GetAllLastErrors(string logDir)
        {
            if (!Directory.Exists(logDir))
                return new[] { $"Directory not found: {logDir}" };

            var logFiles = Directory.GetFiles(logDir, "*.log");
            if (logFiles.Length == 0)
                return new[] { "No log files found." };

            return logFiles.Select(f =>
            {
                var lines = File.ReadAllLines(f);
                return $"{Path.GetFileName(f)}: {(lines.Length > 0 ? lines[^1] : "No error recorded.")}";
            }).ToArray();
        }
    }
}

```
## Gemini Cli 設定檔
* cli 設定檔位置：C:\Users\lio26\.gemini
* 原始gemini cli setting
```json
{
  "theme": "Default",
  "selectedAuthType": "oauth-personal"
}
```
* 修改過後的gemini cli setting
```json
{
  "mcpServers": {
    "MyDotnetServer": {
      "command": "dotnet",
      "args": [
        "D:\\VSProjects\\tool\\MCPServer\\GeminiCliMCPServer\\GeminiCliMCPServer\\bin\\Release\\net8.0\\GeminiCliMCPServer.dll"
      ],
      "cwd": "D:\\VSProjects\\tool\\MCPServer\\GeminiCliMCPServer\\GeminiCliMCPServer",
      "timeout": 30000,
      "trust": true
    }
  },
  "security": {
    "auth": {
      "selectedType": "oauth-personal"
    }
  },
  "ui": {
    "theme": "Default"
  }
}
```

## 使用方式
```shell
> @MyDotnetServer/echo message=123

 ╭───────────────────────────────────────────────────────────────────────────────────────────────────╮
 │ ✓  echo (MyDotnetServer MCP Server) {"message":"123@MyDotnetServer/echo message=123"}             │
 │                                                                                                   │
 │    Echo: 123@MyDotnetServer/echo message=123                                                      │
 ╰───────────────────────────────────────────────────────────────────────────────────────────────────╯
✦ 123@MyDotnetServer/echo message=123

@MyDotnetServer/getLastError logFile="D:\XX\Info\Log\XX_20251007.log"

```
## 參考資料
https://github.com/modelcontextprotocol/csharp-sdk
https://google-gemini.github.io/gemini-cli/docs/tools/mcp-server.html

#gemini #mcp