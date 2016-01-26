環境設置
=========

我們建議讓 Jenkins 採用與開發者相同的環境配置，並且盡量減少對 Jenkins Plugins 的依賴程度。

Jenkins 有許多社群貢獻的第三方 Plugins，且數量持續增加，例如：

- [NodeJS Plugin](https://wiki.jenkins-ci.org/display/JENKINS/NodeJS+Plugin)
- [RVM](https://wiki.jenkins-ci.org/display/JENKINS/RVM+Plugin)

但是就筆者長久使用 Jenkins 的經驗，Plugins 的運作有時並不如預期，安裝過多的 Plugins 可能導致許多問題，Plugins 之間可能也有交互影響的問題。

除非您已經相當瞭解這些 Plugins 的特性，以及可能帶來的副作用，否則並不建議安裝太多 Plugins。

特別是主要的「專案建置流程」，盡可能減少使用 Plugins，讓 Jenkins 與開發者使用同樣的方式建置，例如開發者若使用 `gradle` 指令進行自動化建置及測試：

```
gradle build
```

那麼，讓 Jenkins 做同樣的事情即可，不用特別尋找 Plugins 來用。

實際上絕大多數的建置流程，都可以利用 Jenkins 內建的任務定義方式來完成；如果搭配 Docker 容器技術，更可以大幅化簡開發環境的配置工作。

我們會建議讀者，直接使用執行 Jenkins 服務的「系統使用者帳號」，先把相關所需的環境設置完成。

配置 Jenkins 系統使用者
---------------------

在 Ubuntu Linux 利用 `apt-get` 完成 Jenkins 安裝後，會自動產生名為 `jenkins` 的系統使用者帳號（user）及群組（group）。

/etc/passwd

```
jenkins:x:117:125:Jenkins,,,:/var/lib/jenkins:/bin/bash
```

/etc/group

```
jenkins:x:125:
```

Jenkins 定義的任務，預設會使用 `jenkins` 系統使用者的權限，進行各項指令操作；因此並非所有系統的檔案皆可任意讀寫或執行。

檔案權限的觀念在 Linux 系統中很重要，你在自己或其他帳號的「家目錄」中，所安裝的程式或放置的檔案，並不一定能被 Jenkins 的任務使用。

如果你想讓 Jenkins 能執行一些特定的程式，或是增加一些專屬的配置，例如 `nvm` 或 `~/.profile` 等，需要先切換成 `jenkins` 系統使用者的身份，幫 Jenkins 預先安裝好所需的軟體、配置環境變數等。

在終端機中使用 `su` 指令切換當前的使用者：

```
sudo su - jenkins
```

如此一來，便可以利用 `jenkins` 使用者的身份，進行各項 Jenkins 執行環境相等權限的操作。

使用 `apt-get` 安裝的 Jenkins 其預設的使用者「家目錄」（Home Directory）路徑是：

```
/var/lib/jenkins
```

## 減少對 Jenkins Plugins 的依賴

在測試、除錯及驗證的開發過程中，讓 Jenkins 採用與開發者相同的執行方式與環境配置，將有利於更快速找到問題原因，如果 Jenkins 無法順利完成某個任務，也可以藉由終端機切換 Jenkins 系統使用者的身份方式，進行更進一步的除錯。

過多不必要的 Plugins，反而帶來困擾，不但沒有簡化工作，還可能會增加一些無法預期的問題。

這件事對開發者而言非常重要，因為若每次錯誤發生都要透過 Jenkins 的 Web 操作介面來重新配置任務，重新跑完整個任務流程，過程不僅耗時耗力而且也帶來不少挫折。

相同的，若我們需要增加新的建置程序，也可以直接用 Jenkins 系統使用者進行一次，先驗證過流程沒有問題，再實際加入到任務的設定，如此一來更能夠確保 Jenkins 可以如期正常完成任務！

建立 SSH Keys
-------------

在自動化建置與部署的流程中，我們經常使用 SSH 進行各項操作，例如：

* 複製已建置完成的檔案到遠端伺服器（sftp, scp, rsync）
* 在遠端伺服器執行一段指令（ssh）

平時我們可能採用輸入密碼的方式，進行 SSH 權限的驗證；但是由於 Jenkins 的任務需要自動化執行，此時就需要搭配 SSH 的金鑰驗證（Key Authentication），才能夠在安全無虞的前提下自動完成任務。

### 建立 SSH Key

首先我們需要幫 Jenkins 系統使用者建立專屬的 SSH Key，請先用 `sudo su - jenkins` 切換執行身份。

`ssh-keygen -t rsa`

這條指令預設會在 `~/.ssh` 產生出 `id_rsa` 和 `id_rsa.pub` 兩個檔案。

### 遠端伺服器加入 SSH Key 授權

將 Jenkins 專屬的 `id_rsa.pub` 內容，加入到遠端伺服器的 `~/.ssh/authorized_keys` 內容。

使用 `ssh-copy-id` 指令可以更方便地完成這項任務：

```
ssh-copy-id user@remote
```

透過 SSH Key 就能讓 Jenkins 自動管理多台主機。
