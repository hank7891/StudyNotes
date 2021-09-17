# HEXO 移機教學

 * hexo 重新建置環境。
 * hexo 更換電腦。

<!--  more -->

小弟剛好換新電腦，在此紀錄移植 hexo 編寫環境紀錄。

# 檢查編寫環境
```
# 檢查是否有安裝 git
$ git --version

# 檢查是否安裝 node.js
$ node -v

# 檢查是否有安裝 hexo
$ hexo -v
```

*  若環境沒安裝完全，且忘記怎麼裝了: [點我](/2019/11/29/Hexo/)

# 備份開發環境
備份舊電腦的開發文件
圖 1.

# 新開發環境
將備份檔案放置新電腦後，進到對應資料夾，並用 npm 建置原始檔案編譯。

```
$ cd blog

# npm 建立編譯檔
$ npm install

# 下載 git 工具
$ npm install hexo-deployer-git --save
```

執行看看，看看在本機看看網站有沒有各種毀滅。

```
# 可以透過本機的 http://localhost:4000 查看結果
$ hexo s --debug
```

完成後就可以開始快樂得文章編寫拉!!
