# 專案組成

本章的範例採用 [JHipster](https://jhipster.github.io/) 提供的 Sample Application 為例。

JHipster 的專案由這些開發工具及框架組成：

* Maven
* Grunt
* Spring Boot
* AngularJS 

它可以完整呈現 Maven Project 建置所需的基本任務，包含 war package 和 test 等。

## 建置專案

取得 JHipster Sample Application：

    git clone https://github.com/TrunkWorkshop/jhipster-sample-app.git sample
    
    cd sample

執行：

```
mvn spring-boot:run
```

若沒有錯誤發生，執行結果的訊息會有網址。

```
----------------------------------------------------------
	Local: 		http://127.0.0.1:8080
	External: 	http://127.0.1.1:8080
----------------------------------------------------------
```

用瀏覽器打開 http://127.0.0.1:8080/ 檢視網站畫面。

![](images/jhipster-screenshot.png)
