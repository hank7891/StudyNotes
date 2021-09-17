# GIT 還原單一檔案

* GIT 如何**還原已修改檔案**。
* GIT 如何**將檔案還原至 commit 前版本**。
* GIT 如何**將檔案還原至指定版本**。

<!-- more -->

首先，讓我們看一下 LOG 紀錄。
```
$ git log
```

<圖一>

# 直接**還原已修改檔案**

直接還原即可，以下兩種語法效果相同。
```
1. $ git checkout <file>
2. $ git checkout -- <file>
```

# 還原**已 commmit 檔案**
對於已經 `commit` 上版控(尚未 `push`)，用以下步驟還原。

1. 先用 reset 解除 commit 操作。
```
$ git reset HEAD^
```
如**圖中**，**測試 COMMIT 版本 1** 的紀錄會被移除。並保留其修改內容。
若是對應檔案有在做修改，會以後續修改版本為主。 

2. 再用 checout 還原更改檔案。
```
$ git checkout <file>
```

# 還原**檔案至版控上指定紀錄版本**
可有**圖片**中看到各版本的 `commit Hash`。
使用以下語法還原至對應版本。
```
$ git checkout <commit Hash> <file>
```
小知識: `Hash` 只要取前四碼即可。 


