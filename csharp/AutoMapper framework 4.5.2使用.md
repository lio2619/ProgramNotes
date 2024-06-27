## 下載

* automapper 支援 .net framework 4.5.2的最新版是7.0.1，去nuget下載 automapper 7.0.1
## 註冊

1. 到APP_Start資料夾底下新增一個用來放automapper profile設定檔的檔案
```csharp
using AutoMapper;
using Program.Mapper;

namespace Program.App_Start
{
    public static class AutoMapperConfig
    {
        public static IMapper Mapper { get; private set; }
        public static void Initialize()
        {
            var config = new MapperConfiguration(cfg =>
            {
                cfg.AddProfile<UserProfile>();
            });
            Mapper = config.CreateMapper();
        }
    }
}
```

2. 到Global.asax.cs裡面註冊automapper
```csharp
using Program.App_Start;

namespace ToolPrototype
{
    public class MvcApplication : System.Web.HttpApplication
    {
        protected void Application_Start()
        {
            AutoMapperConfig.Initialize();
        }
    }
}
```

3. 新建資料夾裡面是放實際要mapper的東西
```csharp
using AutoMapper;
using System;
using Program.Models;

namespace Program.Mapper
{
    public class UserProfile : Profile
    {
        public UserProfile()
        {
            CreateMap<string[], User>()
                .ForMember(dest => dest.CustId, opt => opt.MapFrom(src => src[1];
        }
    }
}
```
## 使用
### 一般使用

* 照以下方法使用，這樣出來的變數就會是你所設定的型態
```csharp
using Program.App_Start;
using Program.Models;

string[] testCase = new string[];
var user = AutoMapperConfig.Mapper.Map<User>(testCase);
```

### 特別使用
#### 如果要mapper的class還有其他class

* 用 **.ForMember** 會出現錯誤，所以必須改成 **.ForPath**
```csharp
CreateMap<string[], User>()
	.ForPath(dest => dest.CustId.Name, opt => opt.MapFrom(src => src[1];
```
#### 如果要將額外變數傳進mapper裡面

* 只有 **.ForMember** 可以使用 **ResolveUsing** ，先照以下方法做設定
```csharp
CreateMap<string[], User>()
	.ForMember(dest => dest.CustId, opt => opt.ResolveUsing((src, dest, destMember, context) =>
{
    int count = context.Items.ContainsKey("count") ? (int)context.Items["count"] : 0;
    return $"{src[1]}{DateTime.Now:yyMMdd}{count:D6}{src[8]}{src[10]}";
}))
```

* 在程式碼裡面這樣使用
```csharp
var user = AutoMapperConfig.Mapper.Map<User>(testCase, opts => opts.Items["count"] = startNo + i);
```

#csharp #net #automapper