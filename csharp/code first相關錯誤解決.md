## 錯誤
### 第一種
#### 錯誤訊息
```
System.ArgumentNullException: Value cannot be null.  
Parameter name: type

at System.Activator.CreateInstance(Type type, BindingFlags bindingAttr, Binder binder, Object[] args, CultureInfo culture, Object[] activationAttributes)  
at System.Activator.CreateInstance(Type type, Object[] args)  
at System.Data.Entity.Migrations.Extensions.ProjectExtensions.GetProjectTypes(Project project, Int32 shellVersion)  
at System.Data.Entity.Migrations.Extensions.ProjectExtensions.IsWebSiteProject(Project project)  
at System.Data.Entity.Migrations.Extensions.ProjectExtensions.GetTargetDir(Project project)  
at System.Data.Entity.Migrations.MigrationsDomainCommand.GetFacade(String configurationTypeName, Boolean useContextWorkingDirectory)  
at System.Data.Entity.Migrations.AddMigrationCommand.Execute(String name, Boolean force, Boolean ignoreChanges)  
at System.Data.Entity.Migrations.AddMigrationCommand.<>c__DisplayClass2.<.ctor>b__0()  
at System.Data.Entity.Migrations.MigrationsDomainCommand.Execute(Action command)

Value cannot be null.  
Parameter name: type"?
```
#### 原因
* efcore版本太低
* VS版本太高
#### 解決方式
* 將efcore升到 **6.4.4**
* 開啟VS 2019就可以
### 第二種
#### 錯誤訊息
```
升級 資料表 沒有權限
```
#### 原因
* 可能有好幾個專案，他讀到沒有權限的帳號
#### 決解方式
* 將讀到的那個connect string改成有權限的帳號

## 參考資料
[Entity Framework : Value cannot be null. Parameter name: type - Stack Overflow](https://stackoverflow.com/questions/41777590/entity-framework-value-cannot-be-null-parameter-name-type)
[c# - EF Code First CREATE DATABASE permission denied in database 'master' - Stack Overflow](https://stackoverflow.com/questions/38891256/ef-code-first-create-database-permission-denied-in-database-master)

#csharp #codefirst #error 