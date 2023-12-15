## 綁定datasource

* 如果將datasource綁定後會需要修改/新增的話，要綁定成bindingList才可以做修改
```csharp
var response = dbContext.Allsheetstorages.AsNoTracking().ToList();
BindingList<Allsheetstorage> source = new BindingList<Allsheetstorage>(response);
productDetailData.DataSource = source;
```
* 如果綁定list的話就不能做修改

## 數據龐大讀取速度慢的方法

* 先確定SQL語法的效率，如果確定SQL語法沒問題，就將datagridview裡面的autosizemode改成displaycells，或是其他的也可以，總之不要是allcells就好

## 將datasource新增東西

* 需要注意的是要新增的東西，需要原本就在那個class裡
```csharp
BindingList<Allsheetstorage> dataSource = (BindingList<Allsheetstorage>)((BindingSource)_productDetailData.DataSource).List;
List<Allsheetstorage> allsheetstorages = new List<Allsheetstorage>(dataSource);
allsheetstorages.ForEach(x =>{x.OrderNumber = "0";});
```

#winform #datagridview #csharp