# GIT 查看/匯出差異檔案

* 查看指定 commit 修改過檔案差異。
* 匯出指定 commit 修改過檔案差異

<!-- more -->

# Diff 比對差異檔案

```
$ git diff
```
說明: 比對當下**未進暫存區(Add)**所有檔案區別。

```
$ git diff --cached
```
說明: 比對當下**已進暫存區(Add)**所有檔案區別。

```
$ git diff <filename>
```
說明: 比對當下**未進暫存區(Add)單一檔案**區別。

* 想一想: 那**已進暫存區(Add)單一檔案**區別呢？

---
```
$ git diff <commit-id>
```
說明: 比對**指定 commit 與 HEAD 檔案**區別

```
$ git diff <old commit-id> <new commit-id>
```
說明：比對**兩個 commit** 之間的差異．

## 比較常用的指令集
```
$ git diff HEAD^ HEAD    # 比較最新版與最新版前一次版本的差異
$ git diff ---stat       # 檢視更新的簡略統計資訊。
$ git diff --name-only   # 在更新的訊息後方顯示更動的檔案列表。
$ git diff --name-status #  顯示新增、更動、刪除的檔案列表。
$ git diff --diff-filter= [(A|C|D|M|R|T)…​[*]]] # 配合檔案狀態來篩選顯示檔案列表。
# A = Added
# C = Copied
# M = Modified
# R = Renamed
# T = Changed
# D = Delete
```

讓我們產出差異的檔案清單
```
$ git diff-tree -r --no-commit-id --name-only --diff-filter=ACMRT HEAD
```
 * diff-tree: 比較兩個 commit 之間的差異。
 * -r: 列出完整路徑。
 * --name-only: 不輸出 commit id。
 * --diff-filter=ACMRT: 列出指定類型檔案。
 * HEAD: 當下版本，可改為任一或多個 commit id。

## 將結果輸出為 txt 檔
```
$ git diff-tree -r --no-commit-id --name-only --diff-filter=ACMRT HEAD > test.txt
```

# 匯出差異檔案(含完整路徑)
```
$ git archive --format=zip --output=files.zip HEAD $(git diff-tree -r --no-commit-id --name-only --diff-filter=ACMRT HEAD)
```
* 注意: 若沒加 `$()` 內部篩選，會打包整個專案。

# 小知識
* commid 只要取前六碼就可以了。
* git archive 一定要在版控系統根目錄執行才有作用。

