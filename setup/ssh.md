SSH
===

為 Jenkins User 建立 ssh key
----------------------------

ssh 在自動化的過程扮演很重要的角色，因此我們需要先將 jenkins 的 ssh key 產生出來

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
