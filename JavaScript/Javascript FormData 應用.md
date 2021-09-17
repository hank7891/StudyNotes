# ajax 使用 FormData 上傳檔案

Javascript FormData 應用。
Javascript 傳送 File 檔案。

<!--more-->

# What is FormData?

> 所有向伺服器提交的 HTTP 資料，都是一個表單

FromData 是一種容器，用來模擬表單，向伺服器提交資料，最大的優點是可以傳送二進制文件（File、Blob），簡單來說它就是一個 Object。


建立方式有兩種，第一種是由 HTML 去建立:
```
<form id="Form">
    <input type="text" name="name" value="" />
    <input type="file" name="file" />
</form>

<script>
    var fd = new FormData(document.getElementById("Form"));
</script>

```

注意: 若此處使用 JQuery 去取得 form 表單，會出現錯誤

這是因為 JQuery 取得的是一個數組，而不是 dom 節點，可用以下方式轉換為節點。
```
// $('#Form').eq(0)[0];

<script>
    var fd = new FormData($('#Form').eq(0)[0]);
</script>
```

---
第二種是透過 Javascript 去建立。
```
var fd = new FormData();
fd.append('name', 'YoYo');
```

# 實際應用	
若是要使用 append 方式來放置 file 資料時，可以這麼做。 後端取得方式與 form 表單直接送出無異。
ex: $_FILES(PHP)
```
<form id="Form">
    <input type="text" id="name" name="name" value="" />
    <input type="file" id="file" name="file" />
    <button type="button" id="btn" >test</button>
</form>

<script>
$('#btn').on('click', function () {

    // 資料建置
    var file_data = $('#file').prop('files')[0];
    var fd = new FormData();
    fd.append('file', file_data);
    fd.append('name', $('#name').val());

    // 傳送請求
    $.ajax({
        type: "POST",
        contentType: false,
        processData: false,
        url: url,
        data: fd,
        success: function (data) {
            // TODO
        }
    });
});
</script>

```

# 觀看資料
直接使用 `console.log` 去呈現 `FormData` 是會看不到東西的，我們可以用 `forEach
` 將資料放到另一個 Obj 再做呈現。
```
<form id="Form">
    <input type="text" id="name" name="name" value="" />
    <input type="file" id="file" name="file" />
    <button type="button" id="btn" >test</button>
</form>

<script>
    $('#btn').on('click', function () {
        
        // 資料建置
        var file_data = $('#file').prop('files')[0];
        var fd = new FormData();
        fd.append('file', file_data);
        fd.append('name', $('#name').val());

        // 資料輸出
        var object = {};
        fd.forEach((value, key) => {
            object[key] = value;
        });
        console.log(object)
    });
</script>
```

