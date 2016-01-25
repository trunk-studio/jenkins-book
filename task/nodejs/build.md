build 自動建置
==============

使用時機
--------

1.	daily 建置
2.	週期性建置
3.	進行正式機部署時事先建置

task 實作
---------

設置 git repo 使用： `https://github.com/trunkWorkshop/sailsSample.git`

### shell 指令

```
#!/bin/bash
source ~/.bashrc
cp -r ~/sailsSample/node_modules/ node_modules
npm i
grunt build
zip -r build.zip ./ > /dev/null
```

第一次執行時，可以發現查無 grunt 的問題，此時我們可以 login jenkins user

安裝 grunt-cli 透過：`npm i grunt-cli -g`

再一次執行，完成 build 建置
