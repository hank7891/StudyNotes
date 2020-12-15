# PHP Traits

## What is Traits?

PHP 僅支援單一繼承: 子類別只能繼承單一物件。

若是一個類需要繼承多種行為怎麼辦呢？ Traits 解決了這個問題。

Traits 就是解決在單線繼承的限制下，讓程式碼能夠重複使用。並降低複雜度。

Traits 用於聲明可以在多個 class 中使用的屬性(property)/函式(function)，可以是抽象或是任何可視性(public、protect 、private)，甚至是靜態(abstract)屬性。

## 如何使用
建立語法
```
trait TraitName 
{
  // some code...
}
```

使用語法
```
class newClass 
{
    use TraitName;
}
```

## Example
```
trait message
{
    function msg()
    {
        echo 'Welcome to my home.';
    }
}

class Welcome
{
    use message;
}

$welcome = new Welcome();
$welcome->msg();
```

可以同時使用多個
```
trait messageFriendly
{
    function msg()
    {
        echo 'Welcome to my home.';
    }
}

trait messageQuestion
{
    function msgQuestion()
    {
        echo 'Why are you here?';
    }
}

class Welcome
{
    use messageFriendly, messageQuestion;
}

$welcome = new Welcome();
$welcome->msg();
echo '<br/>';
$welcome->msgQuestion();
```


## 若是名稱重複了呢？
函式名稱重複是會造成錯誤的。

`Fatal error: Trait method msg has not been applied, because there are collisions with other trait methods on...`

需要在使用時就指定要用哪一個的方法。
`insteadof`: 宣告前者為主要使用，要是有多個要全部涵蓋進去哦。
```
trait messageFriendly
{
    function msg()
    {
        echo 'Welcome to my home.';
    }
}

trait messageQuestion
{
    function msg()
    {
        echo 'Why are you here?';
    }
}

trait messageC
{
    function msg()
    {
        echo 'C';
    }
}

class Welcome
{
    use messageFriendly, messageQuestion {
        messageFriendly::msg insteadof messageQuestion, messageC;
    }
}

$welcome = new Welcome();
$welcome->msg();
```

那被替代掉的函式都不能用了嗎？
`as`: 替方法進行別名。
```
trait messageFriendly
{
    function msg()
    {
        echo 'Welcome to my home.';
    }
}

trait messageQuestion
{
    function msg()
    {
        echo 'Why are you here?';
    }
}

class Welcome
{
    use messageFriendly, messageQuestion {
        messageFriendly::msg insteadof messageQuestion;
        messageQuestion::msg as msgQuestion;
    }
}

$welcome = new Welcome();
$welcome->msgQuestion();
```
 * 小提醒: 就算有使用 `as` 進行別名，還是需要先使用 `insteadof` 解重名哦。











