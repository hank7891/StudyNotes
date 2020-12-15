# JavaScript 基礎篇[1]: 變數與資料型別

**JavaScript 基礎** -- 變數與資料型別。

<!--more-->

# 變數
可以將變數想像為一個`盒子`，是用來`存放資料`的。

在 `JavaScript` 中的變數宣告是有規則的，開頭必須是`英文字母`、`底線(_)`或`錢字號($)`，後面可以接著`英文字母`、`底線(_)`或`錢字號($)`以及數字。變數名稱不可以是`保留字(Reserved Words)` 與`關鍵字(keyword)`。

`JavaScript` 是有區分大小寫的，變數 `apple` 與 `Apple` 將會被視為不同的兩個變數。且 `1.3` 版之後支援 `Unicode`。代表著你可以用`中文`來當變數名稱。

但還是避免使用`非英文字母`來做變數名稱命名，用`中文編碼`的話，其他語系系統開啟可能會造成亂碼的情況。

變數在使用前，可以透過 `var` 來進行宣告的動作。在 ES6 之後多了 `let` 與 `const` 兩種。
由於 `JavaScript` 是個 **弱型別[註1]** 的語言，變數本身無需宣告型別，型別的資訊只在值或物件本身。
```
// 透過 var 宣告變數 apple 但沒賦予其值，此時 apple 的內容為 undefined。
var apple;

// 透過 var 宣告變數 apple 且賦予其值，此時 apple 的內容為 'apple'。
var apple = 'apple';
```

若沒宣告變數就要使用的情況下，會出現 `ReferenceError`。 如下: 
```
console.log(hello);
```
![a1](http://zh.mweb.im/asset/img/set-up-git.gif)

或許你會發現，即便沒有用 `var` 進行變數宣告，仍可以定義變數並給予值。但**強烈不建議**這麼做。
因為，**沒有使用 `var` 宣告的變數，全都會變成全域變數**。

**全域變數** 後續再做解說。
```
apple = 'apple';
console.log(apple); // 沒錯，就是 'apple'。
```

**註1:** 程式語言中，是有**型別系統(type system)**的。區分為**強型別**、**弱型別**。
**強型別語言**在定義變數時就必須給予變數**指定型別**，若這個變數做了**錯誤型別**運算，則會出現錯誤。**弱型別語言**則相反，雖然多了許多方便性，但要注意型別轉換時可能產生的非預期錯誤。

# 資料型別
> **變數**沒有型別，**值**才有。

由於 `JavaScript` 是個**弱型別**的程式語言，嚴格來說，**變數**本身其實不帶有資料型別的資訊，其中的**值**或**物件**才有。

`JavaScript` 的型別主要可分為`原始型別(Primitives)`與`物件型別(Object)`。

**原始型別**包含了 `string`、`number`、`boolean`、`null`、`undefined`。而在 ES6 中多了 `Symbol`。
```
typeof true;    // 'boolean'
typeof 'apple'; // 'string'
typeof 123;     // 'number'
typeof { };     // 'object'
typeof [ ];     // 'object'
```

## string 字串
字串需用`單引號 ' '`或`雙引號 " "`包住，兩者不可混用，意思是誰開頭就要誰結尾。 `單引號`與`雙引號`的使用在 `JavaScript` 沒有什麼差異，依習慣使用即可。
```
var str = '我是字串';
var str2 = "我也是字串";
```

若引號不成雙對的話會出狀況，如:
```
var str = 'Let's go!'; // Error
var str = "Let's go!"; // OK
```

如果真的非用**單引號**不可，則可用 `\(跳脫字元 escape character)`處理:
```
var str = 'Let\'s go!'; // OK
```

組合字串用 `+`:
```
var str = 'Hello, ' + 'word.';
```

字串太長需換行銜接可用 `\`:
```
var str = '這是第一行 \
這是第二行 \
這是第三行';
```
注意: `\` 後面不能有東西呦，包含空白。


## number 數字
`JavaScript` 僅有的一種數值的型別，不管整數或小數點都是。
```
var num = 1;
var num = 1.2;
```

特殊的數字 `Infinity (無限大)`、`-Infinity (負無限大)`，以及 `NaN`。
備註:  `NaN` 不是數值。

正數除以 0 會得到 `Infinity (無限大)`，負數除以 0 會得到 `-Infinity (負無限大)`。
```
var num = 1 / 0;  // Infinity
var num = -1 / 0; // -Infinity
```

那 `0/0` 呢？ 結果是 `NaN`。甚至是 `Infinity / Infinity` 或 `-Infinity / -Infinity` 也會都得到 `NaN`。
`NaN` 是個有趣的存在，字面上的意思是 `Not a Number`。但用 `typeof` 來判斷，他又告訴你它是 `number`。
```
console.log(typeof NaN); // number
```

`NaN` 無法做任何數字的運算，結果都會是 `NaN`。也就是說 `NaN` 不屬於任何數字，甚至是自己。
```
NaN === NaN;    // false
```

**WTF...**

所以我們需要 `isNaN` 函示來檢查它:
```
isNaN(NaN);   // true
isNaN(123);   // false
isNaN("123"); // false, 因為字串 "123" 可以透過隱含的 Number() 轉型成數字
isNaN("NaN"); // true, 因為字串 "NaN" 無法轉成數字
```

順帶一提，`JavaScript` 的 `number` 也是基於 `IEEE 754` 來實作。
所以當你執行 `0.1 + 0.2 == 0.3` 時。

p2

為什麼呢！？
這是因為... 自己看 [Why 0.1 + 0.2 !== 0.3](http://0.30000000000000004.com/)

不僅是 `JavaScript` 會產生這種問題，只要是採用 `IEEE 754` 的浮點數編碼方式來表示浮點數時，全都會產生這類問題。


## boolean 布林值 
>JavaScript 中，所有的東西都可以轉換為 boolean。

`boolean` 就簡單多了，其值只有兩種: `true`、`false`。是由發明的科學家 George Boole 命名。

```
var a = true;
var b = false;
var c = (2 > 1); // true
```

## null & undefined
若使用 `Boolean()` 將 `null` 與 `undefined` 轉換為布林值，結果都會是 `false`。但兩者間仍有意義上的差別，故將它們放在一起講。

兩者的共通點是**都只有一種值**，`null` 僅有 `null`，`undefined` 僅有 `undefined`。
```
var a;        // undefined, 宣告卻未給值。
var b = null; // null, 明確給予變數 null。
```


*	`undefined` 代表的是**(此變數) 還沒有給值，所以不知道是什麼**。
*	`null` 代表的是**此變數可能曾經有值)，但現在沒有值**。



也可以使用 `Number()` 強制轉換為數字來看出什麼。
```
Number( null );      // 0
Number( undefined ); // NaN
```

還有一點有趣的事，在**非全域作用範圍下** `undefined` 允許被當成是變數使用。
```
(function() {
  var undefined = 'apple';
  console.log(undefined); // apple
  console.log(typeof undefined); // string
})()
```

甚至是被當成參數來用:
```
(function(undefined) {
  console.log(undefined); // apple
  console.log(typeof undefined); // string
})('apple')
```

我看還是別這樣惡搞你的程式了吧。
~~搞同事的就好！~~

---
# [**基礎篇\[2\]: --->>>**](https://hank7891.github.io/)

