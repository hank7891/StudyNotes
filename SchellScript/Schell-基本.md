# Shell Script - 基礎

將指令寫成檔案，即可讓乏味的重複性工作變得輕鬆。

將命令 `Kernel` 做事的指令寫成一個檔案，就叫做 `Shell Script`。

<!--more-->
 
 
# 介紹

`Shell` 是一種讓使用者可以和作業系統 `Kernel`（核心用來控制 CPU、記憶體、硬碟等硬體）互動溝通的橋樑。`Shell Script` 主要是使用在 `Linux` 和 `MacOS` 等 `Unix-like` 作業系統的自動化操作指令的程式語言。

# Hello World

建立 `.sh` 為副檔名的檔案，並賦予其**執行**權限。
```
# 建造檔案
touch demo.sh

# 賦予權限
chmod -x demo.sh

# 查看權限
ls -l demo.sh

# -rwxr-xr-x
```

實作 Hello World！ 將以下指令寫入指令檔。
```
# 宣告使用 /bin/bash
#!/bin/bash

echo "Hello World.";
```

執行指令檔案
```
./demo.sh
```
[執行結果.jpg]

恭喜你已完成第一隻 `Shell Script`！

# 變數

定義`變數`時，開頭不用給予 `$` 符號但使用變數時就需加上 `$`。並且注意 `=` 前後不能有空白。
```
#!/bin/bash

val=Hello Word.;
val2=$val;

echo $val; # 輸出結果: Hello World.
echo $val2; # 輸出結果: Hello World.
``` 

雙引號 `""` 內容中的特殊字元不會被忽略，而單引號 `''` 中的所有特殊字元將被忽略。也可使用 `\` 跳脫符號將之後的一個字元將被視為普通字串。
```
#!/bin/bash

val="Hello World.";

echo '$val'; # 輸出結果: $val
echo "$val"; # 輸出結果: Hello World.
echo "\$val"; # 輸出結果: $val
```

也可使用`花括弧${}`來將變數包起來，可以了解變數的使用範圍。
```
#!/bin/bash

val="Hello World.";

echo ${$val}; # 輸出結果: Hello World.
```

# 運算
運算符號需用 `(())` 或 `$(())` 包起來，前者在於在於會將**計算結果回傳至原變數中(注意放入多個變數則不會運作)**，後者則是將**計算結果回傳至指定變數中(可放置多個變數)**。
```
#!/bin/bash

val=1;
val1=9;

((val++)) # 此時 val = 2，注意不用加結尾符號
val2=$((val*val1)); # 2 * 9 = 18

echo $val; # 輸出 2
echo $val1; # 輸出 9
echo $val2; # 輸出 18
```

# 判斷式
`Shell` 的判斷式有個潮爆了的特型，那就是**結尾**都是**開頭**的顛倒！
Ex: `if...fi`、`case ... esac`...

先了解比對語法:


語法 | 代表意義
--- | ---
-eq/== | 兩數值相等 (equal)
-ne/!= | 兩數值不等 (not equal)
-gt | n1 大於 n2 (greater than)
-lt | n1 小於 n2 (less than)
-ge | n1 大於等於 n2 (greater than or equal)
-le | n1 小於等於 n2 (less than or equal)


## if...fi
判斷條件放置於`[]`中，前後須留白。

```
#!/bin/bash

x=1;
y=2;

if [ $x == $y ]; then
    echo 'x = y';
elif [ $x -gt $y ]; then 
    echo 'x > y';
elif [ $x -lt $y ]; then
    echo 'x < y';
else
    echo '有本事把我用出來';
fi 
```

## case...esac
```
#!/bin/bash

language='TW';

case ${language} in
    'TW')
        echo '中文';
        ;;
    'EN')
        echo '英文';
        ;;
    *)
        echo '看不懂';
        ;;
esac
```

# 迴圈
跟大多數語言一樣，均可用 `continue(省略後續)`、`break(結束迴圈)`。
若是不小心進入無窮迴圈，可用 `^C` 結束程式。

## for
```
#!/bin/bash

for loop in 1 2 3; do
    echo $loop;
done
```

## while
**條件成立**會持續執行。
```
#!/bin/bash

count=1;

# 1 數到 9 (條件小於 10 執行)
while [ $count -lt 10 ]; do
    echo $count;
    ((count++))
    sleep 0.5;
done
```

## until
**條件不成立**會持續執行。
```
#!/bin/bash

count=10;

# 10 數到 1 (條件不小於 1 執行)
until [ $count -lt 1 ]; do
    echo $count;
    ((count--))
    sleep 0.5;
done
```

# 特殊變數
可以在執行命令檔案時，帶入`參數`並且應用。

使用方式:

指令 | 意義
--- | ---
\$0 | 目前的檔案檔名
\$n | n 從 1 開始，代表第幾個參數
\$# | 傳遞到程式或函式目前有幾個參數
\$* | 傳遞到程式或函式所有參數
\$@ | 類似 $* 但是在被雙引號包含時有些許不同
\$? | 上一個指令退出狀態或是函式的返回值
\$$ | 目前 process PID

```
./demo.sh A B
```

```
#!/bin/bash

echo "$0";
echo "$1";
echo "$#";
echo "$*";
echo "$@";
echo "$?";
echo "$$";
```

執行結果就由各位自行去看囉～

# 總結
此篇文章僅講述一些基本的**語法應用**，有程式底子的人在學 `Shell Script` 並不會太困難。

`Shell Script` 常用於系統管理、自動化操作檔案、自動化重複的指令碼、分析 log 等文件檔案、列印呈現我們想要的資料等...

在熟悉**基礎**後就可以組合出想要的邏輯進而達到有效率的工作行為。

