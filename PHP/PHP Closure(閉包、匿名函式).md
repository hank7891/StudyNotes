# PHP Closure(閉包、匿名函式)

還不知道 `PHP` 有 `Closure`? 那你真的落伍了！

## What is Closure?
Closure: 用於表示`匿名函式`的 `Class`。

閉包減少了`命名空間`的混亂。也讓使用對象之間減少了`相依性`。

`PHP5.3` 開始支援`匿名函式`，讓一些需要彈性的場合更方便。

## 建立匿名函式

注意: 賦予變數`匿名函示`，結尾大括號需要加結尾符號 `;`。
```
$wellcome = function () {
    echo 'Hi, wellcome to my Home ';
};

$wellcome();
```

我們可以透過 use 的宣告語法賦予匿名函式變數。
注意: PHP 7.1 起，不能傳入此類變數：superglobals、 $this 或者和參數重名。
```
$houseCategory = 'villa';
$wellcome = function () use ($houseCategory) {
    echo 'Hi, wellcome to my ' .  $houseCategory . '.';
};

$wellcome();
```

讓我們添加函式的指定參數
```
$houseCategory = 'villa';
$wellcome = function ($name) use ($houseCategory) {
    echo 'Hi ' . $name . ', wellcome to my ' .  $houseCategory . '.';
};

$wellcome('YoYo');
```

會使用了之後，我們馬上用遞迴特性寫一個從 1 加總到指定數字的閉包吧。
```
$fib = function ($n) use (&$fib) {
    if ($n == 0) {
        return 0;
    }

    return $n + $fib($n - 1);
};

echo $fib(10);
```


## 小分享
筆者很常在 `某段邏輯前後的行為` 需要被重複使用時，使用閉包。
例如 sql 的 `Transaction`。
此處程式碼為 Demo 用，無法直接執行。
```
/**
 * sqlTransaction
 *
 * @param \Closure $closure
 *
 * @return mixed
 * @throws Exception
 */
public function sqlTransaction(\Closure $closure){
    $db = \Zend_Db_Table::getDefaultAdapter();

    try{
        $db->beginTransaction();
        $re = $closure();
        $db->commit();

        return $re;
    }catch (Exception $e){
        $db->rollBack();
        throw new Exception($e->getMessage());
    }
}


public function saveData()
{
    $model = $this->_model;
    $this->sqlTransaction(function () use ($data, $model) {
        // TODO 邏輯檢查

        $model->update(data);
        
        // TODO 更新後行為
    });
}


```

## 小知識
* 閉包可利用遞迴特性，取代 foreach 效果。
* 閉包可用於邏輯處理中段需要客製化邏輯時。
* 再叫現代化的 PHP 框架(如 Laravel)中，`閉包`已經是被大量使用的技術。 有興趣可自行去翻閱 Laravel 原始碼。



##### 現在，你學會了嗎！？






