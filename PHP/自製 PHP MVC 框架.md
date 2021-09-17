# 自製 PHP MVC 框架

## 前言
現代 PHP 開發大多使用知名 **Framework** 如: `Zend`、`Laravel`、`Symfony`。
再各 **MVC** 框架作為底層的情況下，產出的程式能較有品質且好維護(當然把 **MVC** 當成**原生結構**寫的大有人在)。

本文透過自製簡易框架的基本結構及邏輯。通常是不會真的用於開發。
然而對新手開發者來說，雖會使用包裝好的 **Framework** 卻不明白背後的運作邏輯。
透過練習可以理解框架的基本運作邏輯，並加以客製化。

<!-- more -->

# MVC
**MVC** 把軟體系統分為三個基本部分：`模型(Model)`、`檢視(View)`和`控制器(Controller)`。

* 模型(Model): 管理大多數**商業邏輯**以及所有的**資料庫連線運作**。


* 檢視(View): 負責**渲染資料**，透過 `HTML` 來呈現畫面。


* 控制器(Controller): 負責響應使用者請求，**準備資料**、**組合邏輯**以及決定如何**展示資料**。


![來源: https://helloacm.com/model-view-controller-explained-in-c/](/images/JaraScriptArticle/WTF.jpeg)

備註: 現代 **MVC** 框架已經將許多功能做更細節的分類了(如 `Laravel` 的 `service container)`)。 但本文僅做最簡單的結構介紹。 熟悉之後各位看官可自行去實作自己的客製化框架。

# 目錄準備
Project 目錄部署

![](/images/JaraScriptArticle/WTF.jpeg)

將伺服器(`Nginx` or `Apache`)的網站根目錄指向 project 內。

# 程式碼規範
* Mysql 的表名需用`全小寫`配合`下劃線(_)` 如: item, acl_menu。

* Models 須用**大寫駝峰式命名**，並在後續串上 `Model` 字樣 如: ItemModel。

* Controllers 須用**大寫駝峰式命名**，並在後續串上 `Controller` 字樣 如: ItemController。

* 方法名(function) 需用**小寫駝峰式命名** 如: index, indexPost。

* Views 呼應 Controllers/function 如: item/index.php

命名規則並無一定，皆可在實作中自行修改/定義。上述規則是為了程式能更好地相互呼叫。

# 重新定向

###Apache: 
透過 `.htaccess` 可以進行部分伺服器請求設定。 一般放在與入口檔案相同資料夾下。
```
<IfModule mod_rewrite.c>
    # 開啟Rerite功能
    RewriteEngine On

    # 如果請求的是真實存在的檔案或目錄，直接訪問
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d

    # 如果訪問的檔案或目錄不是真事存在，分發請求至 index.php
    RewriteRule . index.php
</IfModule>
```

### Nginx:
修改配置檔案，在 `server` 區塊中加入如下。
```
location / {
    # 重新向所有非真是存在的請求到index.php
    try_files $uri $uri/ /index.php$args;
}
```

重新定向有以下用意:

1. 靜態檔案能直接訪問:
    如果檔案或者目錄`真實存在`，則可以直接進行訪問。
    如: static/css/main.css。
    
2. 實作程式單一入口: 
    若是請求地址`不是真實存在`的檔案或目錄，那該請求就會被導向 `index.php(入口網站)` 上。
    如: localhost/item/not.isset
    
    檔案系統中並`不存在`這樣的檔案或目錄，伺服器就會將此請求轉入 `index.php(入口網站)`並將域名之後的變數存入 `REQUEST_URI`。

上述為例，常數 $_SERVER[‘REQUEST_URI’] 會取得 `/item/not.isset`。

# 入口檔案



