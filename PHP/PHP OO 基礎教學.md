# PHP OO 基礎教學

此篇教學只是物件導向的基礎與實作，內容只包含類別與物件的操作，讓不熟悉類別的人可以初識物件導向的好處，並且了解物件與類別的特性與關係。


## 認識物件導向 Object Oriented:

物件導向是一種寫程式的方式，他傾向讓開發者將類似或有關聯性的工作或屬性組織到**類別(class)**裡面。進而讓程式遵循**不重複原則 don’t repeat yourself (DRY)**，且更容易維護。
> “Object-oriented programming is a style of coding that allows developers to group similar tasks into classes.”


## 一、 認識物件(Object)與類別(Class) - Understanding Objects and Classes
首先，先來了解**物件(Object)**與**類別(Class)**的功能及用途。

* 類別(Class)，可以比喻為一棟建築的設計藍圖，清楚的定義了建築的結構及形狀。
* 物件(Object)，可以比喻為一棟真的房子，**物件是類別的實例化**。


而**資料(Data)**就是房子所需要的材料(如 鋼筋、電線、混泥土)若沒有依照**設計藍圖(類別Class)**來組裝，那材料就僅僅是一堆材料。

但當**材料(資料Data)**依照**設計藍圖(類別Class)**來實作後，那這些**材料(資料Data)**就會變成一個有組織且有用的**房子(物件Object)**
> 類別定義了結構以及行為，並且用這些東西打造物件。當多個物件都是由同一個類別產生出來時，每個物件都是一個獨立的個體，且不相依賴的。


## 二、建立類別 Class
建立類別的語法很簡單，使用`class`來定義一個類別，然後在類別名稱後面再加上`大括號{}`
```
<?php
class MyClass
{
    // 類別的屬性與方法要在大括號裡面宣告。
    // Class properties and methods go here
}
```
建立類別後，可以使用 `new` 關鍵字來實例化類別，並存到一個變數上。
```
$obj = new MyClass();
```
使用 `var_dump` 來查看物件內容。
```
var_dump($obj);
```
現在，建立一個 `test.php` 來測試看看吧。
```
class MyClass
{
    // 類別的屬性與方法要在大括號裡面宣告。
    // Class properties and methods go here
}

$obj = new MyClass();
var_dump($obj);
```
贏該會輸出類似畫面(輸出畫面會因環境不同而有些許差別):
```
object(MyClass)[1]
```
這就是一個最簡單的物件形式。你已經完成第一個物件導向程式了。


## 三、定義類別(Class)的屬性(Properties) - Defining Class Properties
使用屬性(Properties)又稱類別的變數(Variable)，用來將資料(Data)存入類別中。
存取用法就跟普通變數一樣，除非這些變數被物件給綁定了，被綁定的變數只能由物件本身存取。

替 `MyClass` 添加一個屬性(Properties):
```
<?php
class MyClass
{
    public $prop1 = "I'm a class property!";
}

$obj = new MyClass();
var_dump($obj);
```

指定要讀取的`物件`以及`屬性`，並將它顯示在瀏覽器上：
```
echo $obj->prop1;
```
> 因為類別可以被實例化為很多個物件。故若無明確指定被實例化的物件，會導致程式碼無法判斷應該讀取哪個物件。

箭頭 `->` 在 PHP 的物件中用來調用物件內的**屬性（Property）**及**方法（Methods）**。

現在，修改 `test.php` 來取得**物件（Property）**內的**屬性（Methods）**。
```
<?php
class MyClass
{
    public $prop1 = "I'm a class property!";
}

$obj = new MyClass();
echo $obj->prop1;
```

重新整理一下你的瀏覽器，得到以下結果：
``` 
I'm a class property!
```


## 四、定義類別(Class)的方法(Methods) Defining Class Methods

方法（Methods）是類別裡面的函式（Functions），物件可以藉由執行這些方法來更動每個物件的行為或狀態。
讓我們建立方法來設置/取得屬性 `$prop1` 的值:

```
<?php
class MyClass
{
    public $prop1 = "I'm a class property!";

    public function setProperty($newval)
    {
        $this->prop1 = $newval;
    }

    public function getProperty()
    {
        return $this->prop1 . "<br />";
    }
}

$obj = new MyClass();
echo $obj->prop1;
```
小筆記
> 物件導向允許物件透過 `$this` 關鍵字來參考自己。物件使用 `$this` 就如同使用物件名稱來指定物件，如： myClass->prop1


要調用這些含有 `$this` 的方法之前，記得要先實例物件。
讀取 `MyClass` 類別的屬性，更改屬性的值。最後再把屬性輸出到瀏覽器上：
```
<?php
class MyClass
{
    public $prop1 = "I'm a class property!";

    public function setProperty($newval)
    {
        $this->prop1 = $newval;
    }

    public function getProperty()
    {
        return $this->prop1 . "<br />";
    }
}

$obj = new MyClass();
echo $obj->getProperty(); // Get the property value


$obj->setProperty("I'm a new property value!"); // Set a new one
echo $obj->getProperty(); // Read it out again to show the change
```
重新整理你的瀏覽器，得到以下結果：
```
I'm a class property!
I'm a new property value!
```
> 當同一個類別被實例化越多次的時候，OOP 的力量也會隨著變得更強大。
> The power of OOP becomes apparent when using multiple instances of the same class.


讓我們來實例化多個類別:
```
<?php
class MyClass
{
    public $prop1 = "I'm a class property!";

    public function setProperty($newval)
    {
        $this->prop1 = $newval;
    }

    public function getProperty()
    {
        return $this->prop1 . "<br />";
    }
}

// Create two objects
$obj = new MyClass;
$obj2 = new MyClass;

// Get the value of $prop1 from both objects
echo 'obj1: ' . $obj->getProperty();
echo 'obj2: ' . $obj2->getProperty();

// Set new values for both objects
$obj->setProperty("I'm a new property value!");
$obj2->setProperty("I belong to the second instance!");

// Output both objects $prop1 value
echo 'obj1: ' . $obj->getProperty();
echo 'obj2: ' . $obj2->getProperty();
```
重新整理你的瀏覽器，得到以下結果：
```
obj1: I'm a class property!
obj2: I'm a class property!
obj1: I'm a new property value!
obj2: I belong to the second instance!
```
物件導向將**物件**視為獨立個體，就如同 150 間房子都是獨立的一樣。
這個特性讓原本要寫 150 次重複的程式碼可以應用**類別多個物件**再設置各自的內部材料(Data)。達到**程式碼不重複原則 ”Don’t Repeat yourself”(DRY)**。

## 封裝 Encapsulation
封裝是以資料為核心，將相關的資料放在一起，把會用到這些資料的方法也放進來。為了和非OO的領域做區隔，OO做了名詞上的改變如：將函式（Function）改為 方法（Method）、將呼叫 （Call）改為調用（Invoke）。
一般會以類別來封裝有相關的行為與資料。

> 對事物的封裝是指，將事物進行抽象後，提供抽象概念的實現的具體方法。


## 五、魔術函數 Magic Methods in OOP
PHP 提供了幾個**魔術函數**讓操作**物件(object)**變得更簡單，這些魔術函數會在物件發生`特定行為時`被呼叫。這讓開發者更容易達成某些有用的任務。

更多魔術函數可以看: [PHP 官方網站的魔術函數文件](https://www.php.net/manual/en/language.oop5.magic.php)

## 使用 Constructor

當一個物件被建立時，它經常需要做一些初始化。PHP 提供了一個 `__construct()` 的魔術函數，當一個物件被建立的時候會被呼叫。

讓我們增加一個 `__construct()` 到 `MyClass`，讓 `MyClass`被實例化的時候，丟出一段訊息：
```
<?php
class MyClass
{
    public $prop1 = "I'm a class property!";

    public function __construct()
    {
        echo 'The class "' . __CLASS__ . '" was initiated!<br />';
    }

    public function setProperty($newval)
    {
        $this->prop1 = $newval;
    }

    public function getProperty()
    {
        return $this->prop1 . "<br />";
    }
}

// Create a objects
$obj = new MyClass;

// Get the value of $prop1
echo $obj->getProperty();

// Output a message at the end of the file
echo 'End of file.<br />';

```
小筆記
> `__CLASS__` 叫做**魔術常數 magic constant**.會回傳被呼叫的類別的名稱。


更多魔術常數可以看: [PHP 官方網站的魔術常數文件](https://www.php.net/manual/en/language.constants.predefined.php)


重新整理你的瀏覽器，得到以下結果：
```
The class "MyClass" was initiated!
I'm a class property!
End of file.
```

## 使用 Destructors
在物件被摧毀的時候呼叫 `__destruct()` 魔術函數，這對於清除一個物件來說很有用(例如：關閉資料庫連線等...）

增加一個 `__destruct()` 到 `MyClass`，讓 `MyClass`被摧毀的時候，丟出一段訊息：
```
<?php
class MyClass
{
    public $prop1 = "I'm a class property!";

    public function __construct()
    {
        echo 'The class "' . __CLASS__ . '" was initiated!<br />';
    }

    public function __destruct()
    {
        echo 'The class "' . __CLASS__ . '" was destroyed.<br />';
    }

    public function setProperty($newval)
    {
        $this->prop1 = $newval;
    }

    public function getProperty()
    {
        return $this->prop1 . "<br />";
    }
}

// Create a objects
$obj = new MyClass;

// Get the value of $prop1
echo $obj->getProperty();

// Output a message at the end of the file
echo 'End of file.<br />';

```
重整頁面，得到訊息:
```
The class "MyClass" was initiated!
I'm a class property!
End of file.
The class "MyClass" was destroyed.
```
小筆記
> 當一個物件使用完畢時，PHP 會自動釋放其記憶體。
> “When the end of a file is reached, PHP automatically releases all resources.”

為了更明確的觸發 `__destruct()` 魔術函數，可以透過 `unset()` 方法來摧毀物件：
```
<?php
class MyClass
{
    public $prop1 = "I'm a class property!";

    public function __construct()
    {
        echo 'The class "' . __CLASS__ . '" was initiated!<br />';
    }

    public function __destruct()
    {
        echo 'The class "' . __CLASS__ . '" was destroyed.<br />';
    }

    public function setProperty($newval)
    {
        $this->prop1 = $newval;
    }

    public function getProperty()
    {
        return $this->prop1 . "<br />";
    }
}

// Create a objects
$obj = new MyClass;

// Get the value of $prop1
echo $obj->getProperty();

// Destroy the object
unset($obj);

// Output a message at the end of the file
echo 'End of file.<br />';
```
重新整理頁面後會顯示以下結果：
```
The class "MyClass" was initiated!
I'm a class property!
The class "MyClass" was destroyed.
End of file.
```

## __toString 將物件轉換為字串
PHP 提供 `__toString()` 魔術函數來避免程式試圖將 `MyClass` 當作字串輸出到瀏覽器上。(被當作字串處理時觸發)

如果把物件當作字串處理的話，在 PHP 中會出現無法轉換型態的錯誤：
```
// Create a new object
$obj = new MyClass;

// Output the object as a string
echo $obj;
```
結果如下：
```
The class "MyClass" was initiated!
Catchable fatal error: Object of class MyClass could not be converted to string in /Applications/MAMP/htdocs/CYOProject/ooptest/test.php on line 40
```

為了避免發生轉換型態的錯誤，加入一個 `__toString()` 函數來做轉換處理：
```
<?php
class MyClass
{
    public $prop1 = "I'm a class property!";

    public function __construct()
    {
        echo 'The class "' . __CLASS__ . '" was initiated!<br />';
    }

    public function __destruct()
    {
        echo 'The class "' . __CLASS__ . '" was destroyed.<br />';
    }

    public function __toString()
    {
        echo "Using the toString method: ";
        return $this->getProperty();
    }

    public function setProperty($newval)
    {
        $this->prop1 = $newval;
    }

    public function getProperty()
    {
        return $this->prop1 . "<br />";
    }
}

// Create a objects
$obj = new MyClass;

// Output the object as a string
echo $obj;

// Destroy the object
unset($obj);

// Output a message at the end of the file
echo 'End of file.<br />';
```

在這個情況下，嘗試將物件轉換成字串的時候，會觸發 `__toString` 函數，再由 `__toString` 函數呼叫 `getProperty()` 方法。重新整理瀏覽器來查看最新的結果：
```
The class "MyClass" was initiated!
Using the toString method: I'm a class property!
The class "MyClass" was destroyed.
End of file.
```

除了本章節提到的 `__construct`、`__destruct`、`__toString` 三個魔術函數以外，還有更多魔數函數可以在 [PHP 手冊](https://www.php.net/manual/en/language.oop5.magic.php) 中可以學習唷！



## 六、類別繼承 Class Inheritance
使用 `extend` 關鍵字可以讓類別繼承其他類別的`方法(methods)`和`屬性(property)`。
範例：建立一個新的類別並且繼承(extends) `MyClass` 類別，新的類別可以使用 `MyClass` 原有的`方法(methods)`和`屬性(property)`：

```
<?php
class MyClass
{
    public $prop1 = "I'm a class property!";

    public function __construct()
    {
        echo 'The class "' . __CLASS__ . '" was initiated!<br />';
    }

    public function __destruct()
    {
        echo 'The class "' . __CLASS__ . '" was destroyed.<br />';
    }

    public function __toString()
    {
        echo "Using the toString method: ";
        return $this->getProperty();
    }

    public function setProperty($newval)
    {
        $this->prop1 = $newval;
    }

    public function getProperty()
    {
        return $this->prop1 . "<br />";
    }
}

class MyOtherClass extends MyClass
{
    public function newMethod()
    {
        echo "From a new method in " . __CLASS__ . ".<br />";
    }
}


// Create a objects
$newobj = new MyOtherClass;

// Output the object as a string
echo $newobj->newMethod();

// Use a method from the parent class
echo $newobj->getProperty();
```
網頁重新整理後，可以看見以下結果：
```
The class "MyClass" was initiated!
From a new method in MyOtherClass.
I'm a class property!
The class "MyClass" was destroyed.
```


## 覆寫(Override) 繼承的方法和屬性
你可以在新類別裡面`重新定義`來更改`繼承的屬性和方法的行為`：
```
<?php
class MyClass
{
    public $prop1 = "I'm a class property!";

    public function __construct()
    {
        echo 'The class "' . __CLASS__ . '" was initiated!<br />';
    }

    public function __destruct()
    {
        echo 'The class "' . __CLASS__ . '" was destroyed.<br />';
    }

    public function __toString()
    {
        echo "Using the toString method: ";
        return $this->getProperty();
    }

    public function setProperty($newval)
    {
        $this->prop1 = $newval;
    }

    public function getProperty()
    {
        return $this->prop1 . "<br />";
    }
}

class MyOtherClass extends MyClass
{
    public function __construct()
    {
        echo "A new constructor in " . __CLASS__ . ".<br />";
    }

    public function newMethod()
    {
        echo "From a new method in " . __CLASS__ . ".<br />";
    }
}


// Create a objects
$newobj = new MyOtherClass;

// Output the object as a string
echo $newobj->newMethod();

// Use a method from the parent class
echo $newobj->getProperty();
```
輸出結果應為複寫後的輸出文字:
```
A new constructor in MyOtherClass.
From a new method in MyOtherClass.
I'm a class property!
The class "MyClass" was destroyed.
```
## 保留父類別的方法 —-範圍解析運算子(scope resolution operator)
通常父類別同名方法的程式碼內容很多，不可能就幾行，如果我們想保留原有的功能，另外再擴展出一點點的功能，但是又不想把原有的程式碼再重寫一次，這樣就可以使用`範圍解析運算子::`來呼叫父類別中被原定義的方法。

於 `__construct` 內使用`範圍解析運算子(scope resolution operator) ::` 來調用父類別原定義的函數：
```
<?php
class MyClass
{
    public $prop1 = "I'm a class property!";

    public function __construct()
    {
        echo 'The class "' . __CLASS__ . '" was initiated!<br />';
    }

    public function __destruct()
    {
        echo 'The class "' . __CLASS__ . '" was destroyed.<br />';
    }

    public function __toString()
    {
        echo "Using the toString method: ";
        return $this->getProperty();
    }

    public function setProperty($newval)
    {
        $this->prop1 = $newval;
    }

    public function getProperty()
    {
        return $this->prop1 . "<br />";
    }
}

class MyOtherClass extends MyClass
{
    public function __construct()
    {
        parent::__construct(); // Call the parent class's constructor
        echo "A new constructor in " . __CLASS__ . ".<br />";
    }

    public function newMethod()
    {
        echo "From a new method in " . __CLASS__ . ".<br />";
    }
}


// Create a objects
$newobj = new MyOtherClass;

// Output the object as a string
echo $newobj->newMethod();

// Use a method from the parent class
echo $newobj->getProperty();
```
輸出結果可見，雖然在 `MyOtherClass` 建構元(__construct)中同時調用了父類別所定義的方法:
```
The class "MyClass" was initiated!
A new constructor in MyOtherClass.
From a new method in MyOtherClass.
I'm a class property!
The class "MyClass" was destroyed.
```
## 七、替屬性和方法加上可視性 Assigning the Visibility of Properties and Methods
加入`可視性(Visibility)`，可以決定能不能從物件外面控制物件的方法和屬性。

可視性有種：`public`、`protected`和`private`。
>替屬性和方法加上可視性，是為了增加對物件的控制。
For added control over objects, methods and properties are assigned visibility.

* Public Properties and Methods
    
    當一個`變數`或`方法`的可視性(Visibility)被宣告為 `public`。這表示這些方法和屬性可以在**類別的裡面與外面被存取**。
    到目前為止的範例中可視性都是宣告為 `public`。
    
* Protected Properties and Methods
    
    當一個`變數`或`方法`的可視性(Visibility)被宣告為 `protected`。該變數或方法只能在**類別以及子類別的內部存取**。
    
    範例：把 `MyClass` 的 `getProperty()` 方法的可視性宣告為 `protected`，並且嘗試從外面呼叫這個方法：
    
```
<?php
class MyClass
{
public $prop1 = "I'm a class property!";

public function __construct()
{
   echo 'The class "' . __CLASS__ . '" was initiated!<br />';
}

public function __destruct()
{
   echo 'The class "' . __CLASS__ . '" was destroyed.<br />';
}

public function __toString()
{
   echo "Using the toString method: ";
   return $this->getProperty();
}

public function setProperty($newval)
{
   $this->prop1 = $newval;
}

protected function getProperty()
{
   return $this->prop1 . "<br />";
}
}

class MyOtherClass extends MyClass
{
public function __construct()
{
   parent::__construct(); // Call the parent class's constructor
   echo "A new constructor in " . __CLASS__ . ".<br />";
}

public function newMethod()
{
   echo "From a new method in " . __CLASS__ . ".<br />";
}
}


// Create a objects
$newobj = new MyOtherClass;

// Use a method from the parent class
echo $newobj->getProperty();
```

執行這段程式碼之後，會出現以下 Call to protected method 錯誤：
```
The class "MyClass" was initiated!
A new constructor in MyOtherClass.
Fatal error: Call to protected method MyClass::getProperty() from context '' in /Applications/MAMP/htdocs/CYOProject/ooptest/test.php line 55
```
接下來，在子類別 `MyOtherClass` 中新增一個 `public` 方法來調用 `getProperty()` ：
```
<?php
class MyClass
{
    public $prop1 = "I'm a class property!";

    public function __construct()
    {
        echo 'The class "' . __CLASS__ . '" was initiated!<br />';
    }

    public function __destruct()
    {
        echo 'The class "' . __CLASS__ . '" was destroyed.<br />';
    }

    public function __toString()
    {
        echo "Using the toString method: ";
        return $this->getProperty();
    }

    public function setProperty($newval)
    {
        $this->prop1 = $newval;
    }

    protected function getProperty()
    {
        return $this->prop1 . "<br />";
    }
}

class MyOtherClass extends MyClass
{
    public function __construct()
    {
        parent::__construct(); // Call the parent class's constructor
        echo "A new constructor in " . __CLASS__ . ".<br />";
    }

    public function newMethod()
    {
        echo "From a new method in " . __CLASS__ . ".<br />";
    }

    public function callProtected()
    {
        return $this->getProperty();
    }
}


// Create a objects
$newobj = new MyOtherClass;

// Call the protected method from within a public method
echo $newobj->callProtected();
```

由結果可見，子類別可以調用父類別可性度為 `protected` 的方法:
```
The class "MyClass" was initiated!
A new constructor in MyOtherClass.
I'm a class property!
The class "MyClass" was destroyed.
```

* Private Properties and Methods

    當一個`變數`或`方法`的可視性(Visibility)被宣告為 `private`。該變數或方法只能在**定義它們的類別內使用**，如果有一個新的類別繼承了宣告有 `private` 屬性或方法的類別，新的類別以及所有的子類別將沒有辦法使用這些被宣告為 `private` 的屬性或方法。
    
範例：將 `MyClass` 的 `getProperty()` 方法的可視度宣告為 `private`，並且使用 `MyOtherClass` 的 `callProtected()` 方法來調用 `getProperty()`方法。
```
<?php
class MyClass
{
    public $prop1 = "I'm a class property!";

    public function __construct()
    {
        echo 'The class "' . __CLASS__ . '" was initiated!<br />';
    }

    public function __destruct()
    {
        echo 'The class "' . __CLASS__ . '" was destroyed.<br />';
    }

    public function __toString()
    {
        echo "Using the toString method: ";
        return $this->getProperty();
    }

    public function setProperty($newval)
    {
        $this->prop1 = $newval;
    }

    private function getProperty()
    {
        return $this->prop1 . "<br />";
    }
}

class MyOtherClass extends MyClass
{
    public function __construct()
    {
        parent::__construct(); // Call the parent class's constructor
        echo "A new constructor in " . __CLASS__ . ".<br />";
    }

    public function newMethod()
    {
        echo "From a new method in " . __CLASS__ . ".<br />";
    }

    public function callProtected()
    {
        return $this->getProperty();
    }
}


// Create a objects
$newobj = new MyOtherClass;

// Call the protected method from within a public method
echo $newobj->callProtected();
```

重新載入瀏覽器，會因為 `private` 調用權限不足而得到錯誤訊息：
```
The class "MyClass" was initiated!
A new constructor in MyOtherClass.
Fatal error: Call to private method MyClass::getProperty() from context 'MyOtherClass' in /Applications/MAMP/htdocs/CYOProject/ooptest/test.php line 49
```

## 靜態/非靜態成員
當一個變數或方法被添加 `static(靜態)`，該變數或方法可以在類別還沒有被實例化就被調用。你可以透過`範圍解析運算子(scope resolution operator) ::` 來調用這些 `static` 屬性或方法。

範例：在 `MyClass` 加入一個 `static` 變數與方法： `$count`、`plusOne()`。
在類別的外面使用 `do…while` 迴圈增加 `$count` 的值：

```
<?php
class MyClass
{
    public $prop1 = "I'm a class property!";
    public static $count = 0;

    public function __construct()
    {
        echo 'The class "' . __CLASS__ . '" was initiated!<br />';
    }

    public function __destruct()
    {
        echo 'The class "' . __CLASS__ . '" was destroyed.<br />';
    }

    public function __toString()
    {
        echo "Using the toString method: ";
        return $this->getProperty();
    }

    public function setProperty($newval)
    {
        $this->prop1 = $newval;
    }

    private function getProperty()
    {
        return $this->prop1 . "<br />";
    }

    public static function plusOne()
    {
        return "The count is " . ++self::$count . ".<br />";
    }
}

class MyOtherClass extends MyClass
{
    public function __construct()
    {
        parent::__construct(); // Call the parent class's constructor
        echo "A new constructor in " . __CLASS__ . ".<br />";
    }

    public function newMethod()
    {
        echo "From a new method in " . __CLASS__ . ".<br />";
    }

    public function callProtected()
    {
        return $this->getProperty();
    }
}

do {
    // Call plusOne without instantiating MyClass
    echo MyClass::plusOne();
} while (MyClass::$count < 10);
```
小筆記
> 當使用範圍解析運算子存取 static 屬性時，記得要在屬性名稱前面加上錢字號 `$`

輸出結果為：

```
The count is 1.
The count is 2.
The count is 3.
The count is 4.
The count is 5.
The count is 6.
The count is 7.
The count is 8.
The count is 9.
The count is 10.
```
    
## 常數定義  
相對於`變數`而言，恆常不變的值而稱作`常數`。在 PHP 中使用 `define()` 宣告。而在類別中則是使用 `const`。
`常數`只能是數值的值，包括`布林`、`整數`、`浮點數`和`字串`。若設為`資源`有可能會出現問題。
`常數`和 `static` 類似，必須直接指定值，但不可運算。可直接透過`範圍解析運算子(scope resolution operator) ::` 來調用。

小筆記
> 常數調用時，直接使用定義名稱即可

範例: 於 MyClass 中定義一個常數 `CLASS_NAME` 並進行呼叫。
```
<?php
class MyClass
{
    const CLASS_NAME  = 'MyClass';

    public $prop1 = "I'm a class property!";
    public static $count = 0;

    public function __construct()
    {
        echo 'The class "' . __CLASS__ . '" was initiated!<br />';
    }

    public function __destruct()
    {
        echo 'The class "' . __CLASS__ . '" was destroyed.<br />';
    }

    public function __toString()
    {
        echo "Using the toString method: ";
        return $this->getProperty();
    }

    public function setProperty($newval)
    {
        $this->prop1 = $newval;
    }

    private function getProperty()
    {
        return $this->prop1 . "<br />";
    }

    public static function plusOne()
    {
        return "The count is " . ++self::$count . ".<br />";
    }
}

class MyOtherClass extends MyClass
{
    public function __construct()
    {
        parent::__construct(); // Call the parent class's constructor
        echo "A new constructor in " . __CLASS__ . ".<br />";
    }

    public function newMethod()
    {
        echo "From a new method in " . __CLASS__ . ".<br />";
    }

    public function callProtected()
    {
        return $this->getProperty();
    }
}

echo 'class name is ' . MyClass::CLASS_NAME;
```
得到結果:
```
class name is MyClass
```

## 八、比較物件導向與直譯程式的差別
兩種撰寫方式間沒有對和錯。只是如果使用物件導向來撰寫程式，在開發大型專案的時候會比較容易管理及維護。



因為物件可以將資料儲存在內部屬性內，因此物件內部的方法不必一直把屬性裝入參數內就可以運行了。
再來，多個屬於同一個類別的物件可以同時存在。這在處理大量數據組合的時候可以把程式變得更加簡化。



>雖然一開始可能令人生畏，但 OOP 確實提供了更簡單的方式來處理資料。
>“While it may be daunting at first, OOP actually provides an easier approach to dealing with data.”



>如果實施正確的話，物件導向會明顯的降低你的工作量。
>“OOP will significantly reduce your workload if implemented properly.”



小叮嚀
>不是每一件事情都需要被物件導向。一個簡單、範圍小的功能是不需要被包裝成一個類別的！撰寫功能時。你必須在物件導向與直譯程式之間好好做個選擇。


## 結語
物件導向運用得正確會讓你的程式變`易讀`、`易維護`、`易攜帶`、`可重複使用`，這會減少你很多花額外的時間。





