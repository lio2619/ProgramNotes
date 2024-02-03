## 安裝

```bash
npm i react-datepicker
```

## 使用

```javascript
import { useState } from "react";
import DatePicker from "react-datepicker";
import 'react-datepicker/dist/react-datepicker.css'  

export default function test() {
  const [startDate, setStartDate] = useState(new Date());
  
  return (
    <DatePicker
      selected={startDate}
      onChange={(date) => setStartDate(date)}
      dateFormat="yyyy/MM/dd"
    />
  );
}
```

## 注意事項

### 跑版

* 如果發現引入 **react-datepicker** 後發現跑版，記得要將以下的程式碼加進去
```javascript
import 'react-datepicker/dist/react-datepicker.css'  
```

### 將選擇日期視窗移到最上層

* z-index 越大代表他就會最越上層
```css
.react-datepicker-popper {
    /*將日期顯示在最上層*/
    z-index: 3;
}
```

### 將使用者選擇的日期輸出

* zh-TW 輸出為 yyyy/mm/dd
* en-GB 輸出為 mm/dd/yyyy
```javascript
const date = startDate.toLocaleDateString('zh-TW');
const date = startDate.toLocaleDateString('en-GB');
```

## 參考資料
[react-datepicker - npm (npmjs.com)](https://www.npmjs.com/package/react-datepicker)
[React Datepicker crafted by HackerOne](https://reactdatepicker.com/#example-calendar-icon-using-react-svg-component)

#react #datepicker