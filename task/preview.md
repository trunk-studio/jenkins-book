preview
=======

task 建置
---------

preview 將會使用到 pm2，同樣是透過 jenkins user 執行下列指令

`npm install pm2 -g`

建置指令
--------

參考 task/[build](buld.md)

透過 ssh 進行 preview
---------------------

### ssh publish setup

-	Name: 選擇在 [publish-over-ssh](../plugin/publish-over-ssh.md) 建置的 ssh server
-	Source files: build.zip
-	Remote directory: deploy/temp

### preview 執行指令

```
rm -rf deploy/preview
mkdir -p deploy/preview
unzip -o deploy/temp/build.zip -d deploy/preview > /dev/null
pm2 kill
pm2 start deploy/preview/app.js
```

如此就可以很快速的將最新的程式碼啟動進行功能驗證

> 只所以這樣處理，因為 preview 跟 production release 非常像，下一個章節將可以直接複製修正
