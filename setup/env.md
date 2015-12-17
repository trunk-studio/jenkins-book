設置建置環境
============

Jenkins 有許多社群貢獻的第三方 Plugins：

- [NodeJS Plugin](https://wiki.jenkins-ci.org/display/JENKINS/NodeJS+Plugin)
- [Rvm](https://wiki.jenkins-ci.org/display/JENKINS/RVM+Plugin)

但是以筆者過去經驗來說，就遇過安裝 Node.js Plugin 就會影響 RVM Plugin 的運作。

除非您已經瞭解這些 Plugins 的特性及可能帶來的副作用，否則並不建議一開始就安裝太多 Plugins。

事實上絕大多數的建置流程，都可以利用 Jenkins 內建的任務定義方式來完成；如果搭配 Docker 來用更可以大幅化簡開發環境的配置工作。

建議的直接使用 jenkins 所設置的 user 把相關的環境設置完成。

確認使用者
----------

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
