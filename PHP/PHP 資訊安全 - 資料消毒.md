### PHP 資訊安全 - 資料消毒

> 荀子-性惡篇第二十三: 人之性惡，其善者僞也。

**永遠不要相信任何來源不明的資料**

<!-- more -->


# 不可信資料來源
只要不是系統產出組合之資料，皆不可信。

如下:
```
 $_GET
 $_POST
 $_REQUEST
 $_COOKIE
 $argv
 php://stdin
 file_get_contents()
 遠端資料庫
 遠端 API
 來自客戶端的資料
```

只要是外部來源資料都有可能是攻擊的源頭(`XSS`、`CSRF`等...)

# 怎麼說呢？

您的網站允許使用`HTML`下評論，那將有可能受到`<script>`隱碼攻擊。

```
<p>This is good!!!</p>

<script>
window.location.href='https://hank7891.github.io/';
</script>
```

您的登入帳號密碼被如此輸入，即會遭受 `SQL Injection`
```
account: ' OR 1=1 #
password: 1234



$account  = $_GET['account']; // '' OR 1=1 #
$password = $_GET['password'];

$query = "SELECT * FROM user WHERE account = '$account' AND　password = '$password'";

產生指令: SELECT * FROM user WHERE account = '' OR 1=1 #AND　password = '1234';
```

如此一來是不是令您毛骨悚然呢？

# 所以呢？
想要開發安全的 Web 應用程式，最重要的是正確掌握資料的**用途**狀態。

* 一般正規化消毒→一般處理用資料
    * 例如：trim、magicquotesgpc、NUL、強制轉型、大小寫轉換、值域範圍檢查、白名單檢查、RegExp規則檢查 
* HTML輸出用消毒→HTML輸出用資料
    * 例如：htmlspecialchars, strip_tags, htmlentities 
* SQL輸出用消毒→SQL輸出用資料
    * 例如：mysqlrealescape_string, addslashes

    --

最重要的是，這些**用途**的資料，應明確加以區別，不要混淆使用，一定要明確配合**用途**進行轉換。
 
所有資料的交換，都應使用**一般處理用資料**來進行，再依資料**用途**進行消毒，避免混用而造成遺忘或重複消毒。 

	






