# 執行 Shell Script

在專案建置過程中，經常需要執行 Shell Script 來完成某些任務，例如：

```
make clean
eb deploy
```

在平時開發階段所使用的各種專案建置指令，只要能用 Shell Script 完成，就可以定義在 Jenkins CI 的任務中。

![](images/shell/add-shell-execution.png)

Jenkins CI 在執行自訂的 Shell Script 時，會帶入以下專案建置所需的各項環境變數。

* BUILD_NUMBER
* BUILD_ID
* BUILD_DISPLAY_NAME
* JOB_NAME
* BUILD_TAG
* EXECUTOR_NUMBER
* NODE_NAME
* NODE_LABELS
* WORKSPACE
* JENKINS_HOME
* JENKINS_URL
* BUILD_URL
* JOB_URL
* SVN_REVISION
* SVN_URL

我們可以利用這些參數，例如產生帶有建置流水號的打包檔。

## 顯示所有環境變數

```
env
```

## 參數化建置


以 JDBC 連線字串為例：

```
JDBC_CONNECTION_STRING
```

## Shell Script 常見指令

在 Jenkins CI 定義 Shell Script，必須「避免太過複雜」。如果真的需要複雜的 Shell 指令，應該先寫成一個 Script 檔案，然後直接執行它。




