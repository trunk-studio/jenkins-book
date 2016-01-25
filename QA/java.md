JAVA project 問題
=================

### 以一個Java Project來說，做什麼樣的調整會最符合Jenkins希望的樣子

-	利用 maven 或是 gradle 進行 auto build
-	test build and production build 盡可能讓一個或少數幾個 command 完成
-	利用 maven task 來定義相關的 task
-	盡可能用 maven repository、減少 local 放置 JAR libraries 檔案
-	若是 java 專案，且又是 web 的話可內嵌 tomcat 或 jetty 方便開發測試
-	部分專案設定配置搭配環境變數作定義
-	盡量讓開發建置環境單純化，避免使用太多需要特別賦予網路存取權限的其他服務

### 很多測試環境需要很多機器的參與，最明顯的就是DB，假設Jenkins要做自動化測試對於資料庫的處置有什麼建議?

-	若有使用 orm (hibernate) 建議可以開 drop 來處理，也就是每次都新建資料庫
-	自動化測試必須要讓資料庫隨時有新的開始
-	沒有 orm 也應該要使用 sql script 來初始資料
-	如果專案允許，搭配 H2 / sqlite 等輕量化資料庫引擎並搭配 test 環境的配置與初始化資料
