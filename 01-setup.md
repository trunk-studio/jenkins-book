設置建置環境
============

Jenkins 有許多社群貢獻的第三方 Plugins：

- [NodeJS Plugin](https://wiki.jenkins-ci.org/display/JENKINS/NodeJS+Plugin)
- [Rvm](https://wiki.jenkins-ci.org/display/JENKINS/RVM+Plugin)

但是以筆者過去經驗來說，就遇過安裝 Node.js Plugin 就會影響 RVM Plugin 的運作，安裝過多的 Plugins 可能導致許多問題。

除非您已經瞭解這些 Plugins 的特性及可能帶來的副作用，否則並不建議一開始就安裝太多 Plugins。

事實上絕大多數的建置流程，都可以利用 Jenkins 內建的任務定義方式來完成；如果搭配 Docker 來用更可以大幅化簡開發環境的配置工作。

一般來說，我們建議直接使用執行 Jenkins 程式的使用者帳號，把相關所需的環境設置完成。

配置 Jenkins 使用者的環境
--------------------------

在 Ubuntu Linux 利用 `apt-get` 完成 Jenkins 安裝後，會自動產生名為 `jenkins` 的系統使用者帳號（user）及群組（group）。


`/etc/passwd`

```
jenkins:x:117:125:Jenkins,,,:/var/lib/jenkins:/bin/bash
```

`/etc/group`

```
jenkins:x:125:
```

在 Jenkins 定義的任務，預設會使用 `jenkins` 使用者的權限進行操作，因此並非所有的檔案皆可任意讀寫或執行。

檔案權限的觀念在 Linux 系統中很重要，你在自己或其他帳號的家目錄中安裝的程式或放置的檔案，並不一定能夠被 Jenkins 的任務使用。

如果你希望幫 `jenkins` 帳號增加一些專屬的配置，需要在終端機中使用 `sudo su jenkins` 可以切換成 `jenkins` 使用者的身份進行各項操作，該 user 的家目錄（Home Directory）位置是 `/var/lib/jenkins`。

### 不使用 plugin 來安裝相關 library 的好處

除了 task 的執行之外，另外一個原因是，在除錯的過程中讓 jenkins CI 跟 jenkins user 同樣環境設置方式將會有利於加速確認環境是否正確或是有異常時可以直接用 jenkins user 進行 debug

這件事非常重要，因為若都只能用 task 確認，每次確認結果將會比較慢，執行上會比較有挫折感。

相同的，若我們需要新增新的處理，也可以進行直接用 jenkins user 進行，將會更直接的把自動化需求完成，一旦確認沒有問題 理論上再把相關指令讓 jenkins CI 執行就會正確！

TDD 的精神無誤。
SSH
===

為 Jenkins User 建立 SSH Keys
-----------------------------

SSH 在自動化的過程扮演很重要的角色，因此我們需要先將 jenkins 的 ssh key 產生出來

### 透過 jenkins user 建立 ssh key

`ssh-keygen -t rsa`

default 會產生在 `~/.ssh` 將會有 `id_rsa`, `id_rsa.pub` 這兩個檔案

### 將建立好的 public key 加入到要傳輸的目標機器

`cat ~/.ssh/id_rsa.pub >>~/.ssh/authorized_keys`

有了 ssh key 以便後續自動化進行處理，在 jenkins user 底下執行上述指令，也就表示：

> 把本機當作 stage machine

這樣做的好處是，一旦 stage machine 在其他位置

只要改變 ssh server ip 並且再把 id_rsa.pub 加入對象機器即可，其他程序皆相通

設定 credentials
----------------

![](images/ssh/createDomain.png)

![](images/ssh/createCredentials.png)

新增 ssh server
---------------

我們可以先把 jenkins CI server 視為 development 測試環境，因此我們需要進行 ssh server 相關設置

相關設置參考：plugin/[publish over ssh](../plugin/publish-over-ssh.md) 透過該章節設置，我們可以確保 ssh 連結正常
設置安全性
==========

設置畫面
--------

![](images/security/setup.png)

專案型矩陣授權策略
------------------

### 使用時機

希望可以控管特定 task 可被特定人員存取，例如：production deploy 時，只有 DevOps 人員可以進行 release task 的執行

### 設置方式

在 `Jenkins > 設定全域安全性` 使用 `專案型矩陣授權策略` 並且在新增人員至少要有整體 `read` 權限，如下圖：

![](images/security/project-read.png)

需要注意的是，若使用者有設置 `整體 Administer` 權限，預設將可以看到所有的 task。

接著，我們可以進入特定 task 進行權限設置，如下圖：

![](images/security/task-setting.png)

最後再使用 test 這個 user 進行登入後，將只能看到有設置可以存取的 task 被顯示出來

![](images/security/result.png)
時區設置
========

在 `/etc/default/jenkins` 加入下面設定：

`JAVA_ARGS="-Dorg.apache.commons.jelly.tags.fmt.timeZone=Asia/Taipei"` -

參考：http://blog.blackbing.net/post/2014/03/07/jenkins-notes
Master/slave
============

節點套件安裝
------------

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install default-jre
```

節點使用者設定 ssh
------------------

新增你要用來執行 slave 的 user，e.g. slave

參考 [ssh](./ssh) 進行設定

jenkins slave 設置
------------------

![](images/master_slave/setting.png)

slave 無網路情形
----------------

可以使用 `在 Master 上執行指令啟動 Slave`

參考 jenkins 內的說明

> 啟動 Slave 代理程式的指令，可以控制 Slave 電腦並與 Master 溝通。 Jenkins 假設執行的程式會在正式的 Slave 機器上啟動 slave.jar。
>
> 可以由 http://${jenkinsServerHost}/jnlpJars/slave.jar 下載 slave.jar。
>
> 簡單一點就像 "ssh 主機名稱 java -jar ~/bin/slave.jar"。 但是，一般會建議您在 Slave 上面寫一個小 Shell Script，控制 Java 及 slave.jar 的位置， 也能設定 PATH 這類節點間不盡相同的環境變數。就像:
>
> #!/bin/sh exec java -jar ~/bin/slave.jar
>
> 您可以使用任何指令執行 Slave 機器上的程式，例如 RSH。 只要最後程式的 stdin 及 stdout 被連到 "java -jar ~/bin/slave.jar" 就好。
>
> 大型部署環境下，可以考慮從掛載 NFS 的共通位置中載入 slave.jar， 就不用每次升級 Jenkins 時還要同步更新每部機器上的這個檔案。
>
> 設定成 "ssh -v 主機名稱" 可以幫助您處理連線問題。
