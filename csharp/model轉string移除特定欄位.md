## model

```csharp
public class Person
{
	public string name {get; set;}
	public Address address {get; set;}
}

public class Address
{
	public string code {get; set;}
	public string road {get; set;}
}
```
## 靜態移除

* 如果只是不想讓某個欄位被轉為string照者以下的程式碼就可以了
```csharp
public class Person
{
	public string name {get; set;}
	public Address address {get; set;}
}

public class Address
{
	public string code {get; set;}
	[JsonIgnore]
	public string road {get; set;}
}
```
## 動態移除

* 如果在某些情況需要有就要用以下的程式碼
```csharp
Person person = new Person();
JObject jsonObject = JObject.FromObject(person);
if (jsonObject["address"] is JObject innerObject)
{
	innerObject.Remove("road");
}
string p = Newtonsoft.Json.JsonConvert.SerializeObject(jsonObject);
```

#json #csharp #net 