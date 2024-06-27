## 下載

* 請在nuget安裝最新版的automapper
## 註冊

1. 到Progran.cs裡面註冊automapper，記得要在builder.Build()之前
```csharp
builder.Services.AddAutoMapper(AppDomain.CurrentDomain.GetAssemblies());
```

2. 新建資料夾裡面是放實際要mapper的東西
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
using AutoMapper;
using Program.Models;

private readonly IMapper _mapper;
var response = _mapper.Map<User>(originRequest);
```

### 特別使用
#### 如果要mapper的class還有其他class

* 用 **.ForMember** 會出現錯誤，所以必須改成 **.ForPath**
```csharp
CreateMap<string[], User>()
	.ForPath(dest => dest.CustId.Name, opt => opt.MapFrom(src => src[1];
```
#### 如果要將額外變數傳進mapper裡面

* 在automapper 8.0.0 之後resolveusing被棄用了，改成以下方法
```csharp
CreateMap<string[], User>()
	.ForMember(dest => dest.CustId, opt => opt => opt.MapFrom((src, dest, context) => context.Items["UserName"]));
```

* 在程式碼裡面這樣使用
```csharp
var user = AutoMapperConfig.Mapper.Map<User>(testCase, opt => opt.Items["UserName"] = context["UserName"]);
```

#csharp #net #automapper