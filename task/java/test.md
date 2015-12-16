test
====

延續 task/[build](task/build.md)

我們可以建置透過 build task 直接複製如下圖：

![](images/test/addTestTask.png)

建置指令
--------

```
#!/bin/bash
source ~/.bashrc
mvn clean
cp -r ~/node_modules ./ > /dev/null
mvn clean install test
```

設置 test report 呈現測試結果
-----------------------------

report 位置：`target/surefire-reports/*.xml`

執行結果
--------

參考 [report plugin](../../common/test-report.md)
