## 問題

![[Pasted image 20241115112300.png]]
* 看起來是因為automapper對到錯誤的東西，所以才會發生錯誤
## 解決

```csharp
services.AddAutoMapper(cfg => cfg.ShouldMapMethod = (m => false));
```
* 加入以上程式碼就可以正常執行了
* 這個的版本如以下圖片
![[Pasted image 20241115112107.png]]

* 看網路上他們是說如果是automapper11.0.0以上要用以下程式碼解決
```csharp
```csharp
using AutoMapper;
using AutoMapper.Internal;

var mapperConfig = new MapperConfiguration(mc =>
{
    mc.Internal().MethodMappingEnabled = false;
    mc.AddProfile(new MappingProfile());
});
```

Dependency injection:

```csharp
services.AddAutoMapper(cfg => cfg.Internal().MethodMappingEnabled = false, typeof(MaappingProfile).Assembly);
```

## 參考資料
[MaxInteger[T](System.Collections.Generic.IEnumerable1[T])' violates the constraint of type parameter 'T' exception · Issue #3988 · AutoMapper/AutoMapper · GitHub](https://github.com/AutoMapper/AutoMapper/issues/3988)

[[dotnet-sdk-7.0.100-preview.5.22257.3] MaxInteger[T](System.Collections.Generic.IEnumerable1[T])' violates the constraint of type parameter 'T' exception error · Issue #69119 · dotnet/runtime](https://github.com/dotnet/runtime/issues/69119)

[c# - System.DateTime on 'T MaxInteger[T](System.Collections.Generic.IEnumerable1[T])' violates the constraint of type T for .NET 7 using AutoMapper 11.0.1 - Stack Overflow](https://stackoverflow.com/questions/74730425/system-datetime-on-t-maxintegertsystem-collections-generic-ienumerable1t)



#net #automapper #error 