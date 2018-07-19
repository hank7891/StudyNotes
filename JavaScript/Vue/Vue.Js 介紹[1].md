# Vue.Js 是什麼?
Vue(讀音 vjuː，類似**view**)，是一套構建用戶界面的**漸進式框架**(The progressive framework)。與其他大型框架不同的是，Vue被設計為可由底向上逐漸應用。Vue的核心只關注圖層，不僅易於上手，還便於與第三方套件項目整合。
另一方面，當與現代化工具鍊結合使用時Vue能對html進行高度渲染，也完全能為復染的單頁應用提供驅動。

```
如果你剛開始學習前端開發(html、CSS、JavaScript)，將框架作為學習的第一步可能不會是個好主意。
 建議掌握好基礎知識在進行較複雜的框架應用學習。
```

# 起步
首先須建立一個可執行頁面檔案並載入vue.js。

### 基本php檔案
教學開發筆者使用CDN Vue.Js做線上載入動作。
相關網址可至[CDN Vue.Js](https://cdnjs.com/libraries/vue)自行挑選及使用。
```
<!DOCTYPE html>
<html>
<head>
	<script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.16/vue.js"></script>
</head>
<body>

</body>
</html>
```

# 聲明式渲染
Vue.js的核心採用簡潔的模板語法來將數據渲染進DOM的系統。
先建立相關初始介面。

div:
```
<div id="app">
	{{ message }}
</div>
```

script:
```
var app = new vue({
	el: '#app'
	data: {
		message: 'Hello Vue!'
	}
});
```

組合起來大概長這樣:
```
<!DOCTYPE html>
<html>
<head>
	<script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.16/vue.js"></script>
</head>
<body>

<div id="app">
	{{ message }}
</div>
<script>
var app = new Vue({
	el: '#app',
	data: {
		message: 'Hello Vue!'
	}
});
</script>

</body>
</html>
```

完成後至頁面觀看應該可以看到 `Hello Vue!`字眼。恭喜你建立第一個Vue應用。
現在類別數據與DOM已經被建立關聯，所有關聯都是**響應式**的。怎麼確認呢？
打開瀏覽器的Javascript控制台(在該實作頁面下)。修改 `app.message`的值，就會看到相對應的結果修改了。

除了本文插值，還可以像這樣來綁定元素:
先賦予內文顯示標籤屬性順便使用Vue綁定元素。
```
<span v-bind:title="message_title">
        {{ message }}
</span>
```
在剛剛建立app類別內賦予`message_title`值
```
data: {
	message: 'Hello Vue！',
	message_title: '看見我了嗎'
}
```

完成後大概長這樣:
```
<!DOCTYPE html>
<html>
<head>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.16/vue.js"></script>
</head>
<body>
<div id="app">
    <span v-bind:title="message_title">
        {{ message }}
    </span>
</div>
<script>
var app = new Vue({
    el: '#app',
    data: {
        message: 'Hello Vue！',
        message_title: '看見我了嗎'
    }
});
</script>
</body>
</html>
```
講鼠標移至Hello Vue!字樣上晃個幾下。
應該可以看到 `看見我了嗎` 提示字眼。
如果打開瀏覽器的JavaScript控制台修改`app.message_title`內容，依然可看到綁定之`span title`被動態更改。

這邊新增的`v-bind`特性被稱為**指令**。指令帶有前綴`v-`，已表示它們是**Vue**提供的特殊特性。作用是在渲染的DOM上應用特殊的響應式行為。使`title`與`message`屬性保持一致。

# 條件與循環
控制元素的顯示也很簡單可使用`v-if`配額類別屬性:
```
<span v-if="seen">
	你看不見我
</span>
```
```
data: {
	seen: false
}
```
添加後正常頁面上應該是看不到的。
但只要至控制台輸入`app.seen=true`，就會變魔術般將訊息顯示出來了。

注意綁定方法的參數均要在初創Vue類別所指定的範圍內(#app)。
由上述例子可以了解到，Vue不僅可以把數據綁定到DOM本文或特性，還可以綁定到結構裡，此外Bue也提供強大的過度效果系統，可以在Vue 插入/更新/移除元素時自動應用[過度效果](https://cn.vuejs.org/v2/guide/transitions.html)。

還有其他許多指令，都有特殊功能。例如`v-for`可以綁定數組的數據來渲染一格項目列表:
```
    <ol>
        <li v-for="todo in todos">
            {{ todo.text }}
        </li>
    </ol>
```
```
data: {
	todos: [
		{'text': '測試1。'},
		{'text': '測試2。'},
		{'text': '測試3。'},
	]
}
```
當然這也是響應式的。
試試看在控制器輸入 `app.todos.push({text: 'Text New Title.'})`。


上述例子皆可看出Vue對html高度渲染的方便性。
動態是下拉式選單生成 **Vue**僅需使用`v-for`即可完成。
利用`input text`影響其他DOM欄位值，只需雙向綁定相關原件即可。
若善用Vue.js的渲染能力。能夠快速且有效的開發系統前端架構。
當然Vue還提供其他進階類型的應用。

最後附上此篇產出後的完整code:
```
<!DOCTYPE html>
<html>
<head>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.16/vue.js"></script>
</head>
<body>
<div id="app">
    <span v-bind:title="message_title">
        {{ message }}
    </span>
    <br />
    <span v-if="seen">
        你看不見我
    </span>
    <br />
    <ol>
        <li v-for="todo in todos">
            {{ todo.text }}
        </li>
    </ol>
</div>

<script>
var app = new Vue({
    el: '#app',
    data: {
        message: 'Hello Vue！',
        message_title: '看見我了嗎',
        seen: false,
        todos: [
            {'text': '測試1。'},
            {'text': '測試2。'},
            {'text': '測試3。'},
        ]
    }
});
</script>
</body>
</html>
```
\\
\\
## 參考網站
[Vue官網教學](https://cn.vuejs.org/v2/guide/index.html)

[Vue官網過度效果教學](https://cn.vuejs.org/v2/guide/transitions.html)

[Vue CDN](https://cdnjs.com/libraries/vue)

[漸進式框架](https://medium.com/@gotraveltoworld/vue-js-%E4%BD%95%E8%AC%82%E6%BC%B8%E9%80%B2%E5%BC%8F%E6%A1%86%E6%9E%B6-7d0281a7efa9)