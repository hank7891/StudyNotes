

----
# 使用 HTML 取得本地檔案
```
<input type="file" id="testFile" />
```
**File API** 可以從 **File** 物件中讀取 **FileList** ，**FileList** 內包含使用者所選取的檔案。
如果使用者只選擇一個檔案，那麼我們只需要考慮第一個檔案物件。

# 使用 DOM 獲取選擇的檔案

HTML: 
```
<input type="file" id="testFile" />
```

JS:
```
var file = document.getElementById('testFile').files[0];
```

# 使用 [JQUERY](https://jquery.com/) 獲取選擇的檔案

HTML: 
```
<input type="file" id="testFile" />
```

JS:
```
var file = $('#testFile').get(0).files[0];
```

# 使用 change event 獲取選擇的檔案

HTML: 
```
<input type="file" id="testFile" onchange="selectFile(this.files)" />
```

JS:
```
function selectFile(files) {
    var file = files[0];
}
```

# 獲得選取的檔案資訊

上述的例子顯示獲取在檔案清單裡所有檔案物件的方法。
**File** 提供三個包含檔案重要訊息的屬性。

* `name`: 唯讀的檔案名稱，並未包含檔案路徑。
* `size`: 為 64 位元的整數，用以表示檔案的 byte 的長度。
* `type`: 為唯讀字串。表示檔案的 MIME-type 。若是無法取得檔案的 Mime-type ，則其值會是一個空字串 ""。

# 使用 FileReader 讀取文件內容

### 讀取文字
HTML: 
```
<input type="file" onchange="selectTextFile(this.files)" />
<p id="showText"></p>
```

JS:
```
function selectTextFile(files) {
    if (!files.length) {
        return false;
    }
    
    let file    = files[0];
    let reader = new FileReader();
    reader.onload = function () {
        document.getElementById('showText').src = this.result;
    };
    
    reader.readAsText(file);
}
```

### 當然也可以讀取圖片
HTML: 
```
<input type="file" onchange="selectImgFile(this.files)" />
<img id="showImg"></img>
```

JS:
```
function selectImgFile(files) {
    if (!files.length) {
        return false;
    }
    
    let file   = files[0];
    let reader = new FileReader();
    reader.onload = function () {
        document.getElementById('showImg').src = this.result;
    };

    reader.readAsDataURL(file);
}
```

---

[Code Demo](https://github.com/hank7891/HtmlJsInputFileShow)


