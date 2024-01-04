## pip

```powershell
pip install pytesseract
```

## 下載程式

1. 去 [Home · UB-Mannheim/tesseract Wiki (github.com)](https://github.com/UB-Mannheim/tesseract/wiki) 這邊下載新版的執行檔
2. 如果需要辨識繁體中文去 [tessdata_best/chi_tra.traineddata at main · tesseract-ocr/tessdata_best (github.com)](https://github.com/tesseract-ocr/tessdata_best/blob/main/chi_tra.traineddata) 這邊下載訓練資料，並且把資料丟到下載的執行檔裡面一個叫tessdata的地方

## 使用

```python
#圖片轉文字
import pytesseract
def GetPhotoText(img):
    """將圖片轉成文字"""
    pytesseract.pytesseract.tesseract_cmd = r'D:\tesseract\tesseract.exe'
    text = pytesseract.image_to_string(img, lang='chi_tra')
```

* pytesseract.tesseract_cmd 後面接妳執行檔下載的地方
* 文字辨識預設為英文，要辨識中文後面要接 **lang='chi_tra**
* image_to_string 會輸出辨識的文字
* image_to_data 會輸出每一個辨識文字的位置、準確率...

#python #OCR