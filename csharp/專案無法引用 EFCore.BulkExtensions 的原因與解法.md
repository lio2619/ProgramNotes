## 問題
* 在安裝**EFCore.BulkExtensions**套件後，在專案裡面沒有辦法引用他
* 以下為當時出現問題的csproj
```xml
<Project Sdk="Microsoft.NET.Sdk"> 
	<PropertyGroup> 
		<OutputType>Exe</OutputType> 
		<TargetFramework>net8.0</TargetFramework> 
		<ImplicitUsings>enable</ImplicitUsings> 
		<Nullable>enable</Nullable> 
	</PropertyGroup> 
	<ItemGroup> 
		<PackageReference Include="Dapper" Version="2.1.66" /> 
		<PackageReference Include="EFCore.BulkExtensions" Version="9.0.1" /> 
		<PackageReference Include="Npgsql.EntityFrameworkCore.PostgreSQL" Version="9.0.4" /> 
	</ItemGroup> 
</Project>
```
## 解決方式
* 原因是因為此專案為.net 8，但是**EFCore.BulkExtensions**、**Npgsql.EntityFrameworkCore.PostgreSQL**都安裝到.net 9的版本，所以才會出現專案沒有辦法引用的問題
* 以下為解決後的csproj
```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net8.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Dapper" Version="2.1.66" />
    <PackageReference Include="EFCore.BulkExtensions" Version="8.0.4" />
    <PackageReference Include="Npgsql.EntityFrameworkCore.PostgreSQL" Version="8.0.4" />
  </ItemGroup>

</Project>
```

#net #nuget 