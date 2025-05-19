## 原因

* 以下所有的編碼都是 **utf-8**
* 當字串裡面有難字時，將字串傳入getbyte的程式碼裡面將每次或的byte相加起來會是 6 個 **byte**，如果將該字串一個字元一個字元的塞入 **stringbuilder** 會是 4 個 **byte**
* 這樣就會照成程式碼上面出錯的問題
* 難字指的是由兩個片段所組合出來的文字

## 原始程式碼

* 以下的程式碼會照成難字判斷的問題
```csharp
var index = 0;
var sb = new StringBuilder();
foreach (var c in value)
{
	var b = encoding.GetBytes(c.ToString());
	if (index < startIndex && index + b.Length > startIndex)
	{
		var startSpaceLength = index + b.Length - startIndex;
		sb.Append("".PadLeft(startSpaceLength));
	}
	else if (index < startIndex + length && index + b.Length > startIndex + length)
	{
		var endSpaceLength = index + b.Length - startIndex;
		sb.Append("".PadLeft(endSpaceLength));
	}
	else if (index + b.Length > startIndex && index + b.Length <= startIndex + length)
	{
		sb.Append(c);
	}
	index += b.Length;
	if (index > startIndex + length) break;
}
var result = encoding.GetString(encoding.GetBytes(sb.ToString()), 0, length);
return result;
```

## 解決方法

* 在 **.net framework** 可以用 **StringInfo** 去解決該問題
* 如果是在 **.net 8**的環境可以用 **rune** 去解決
* 以上兩種都是微軟內建的方法，雖然效率會比較慢但是可以解決
* 如果確定傳入的字串不會有 **難字** 、**表情符號** 之類的東西用上面的方法就好
```csharp
var index = 0;
var sb = new StringBuilder();

var enumerator = StringInfo.GetTextElementEnumerator(value);

while (enumerator.MoveNext())
{
    var textElement = enumerator.GetTextElement();
    var b = encoding.GetBytes(textElement);

    if (index < startIndex && index + b.Length > startIndex)
    {
        sb.Append(' ', index + b.Length - startIndex);
    }
    else if (index < startIndex + length && index + b.Length > startIndex + length)
    {
        sb.Append(' ', index + b.Length - startIndex);
    }
    else if (index + b.Length > startIndex && index + b.Length <= startIndex + length)
    {
        sb.Append(textElement);
    }

    index += b.Length;

    if (index > startIndex + length)
        break;
}

var resultBytes = encoding.GetBytes(sb.ToString());
return encoding.GetString(resultBytes, 0, length);
```


## 為什麼StringInfo可以正常的處理 難字

* 因為難字的兩個 char 的 Unicode 會在正常 char 的外面，因此他可以判斷目前這個char是不是正常的，如果不是就往後看看能不能將目前的 char 跟 後面的 char 組合在一起變成難字。
## 參考資料
.net framework [StringInfo](https://learn.microsoft.com/zh-tw/dotnet/api/system.globalization.stringinfo?view=net-8.0)
.net 8 [Rune](https://learn.microsoft.com/zh-tw/dotnet/api/system.text.rune?view=net-8.0)

#csharp #byte #char

