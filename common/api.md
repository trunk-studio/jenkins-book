jenkins api 使用
================

可以參考

https://github.com/jansepar/node-jenkins-api

api 有：

-	lastBuild
-	lastStableBuild
-	lastSuccessfulBuild
-	lastFailedBuild
-	lastUnstableBuild
-	lastUnsuccessfulBuild
-	lastCompletedBuild

常用 API
--------

### last success: 取得最後建置版號

http://localhost:port/job/build/lastSuccessfulBuild/api/json

使用於取得版號資訊，以及 changelog
