Publish over SSH
================

使用時機：

1.	專案建置完成後需要傳輸到 production 機器時
2.	每日建置完成後需要傳到別台機器進行備份時
3.	檔案傳輸完成後，需要透過遠端機器進行後續指令執行時

使用前準備
----------

1.	透過 jenkins user 建立 ssh key

	`ssh-keygen -t rsa`

2.	將建立好的 public key 加入到要傳輸的目標機器

	`cat ~/.ssh/id_rsa.pub >>~/.ssh/authorized_keys`

plugin 相關設定
---------------

進入 jenkins 後台設定，移至 `Publish over SSH` 區塊

Key 的部分需要傳入剛剛建立好的 private key

`cat ~/.ssh/id_rsa`

name 為在 jenkins task 設定時識別名稱 hostname 則為目標機器位置 username 則是你要透過 ssh 登入的使用者帳號 Remote Directory 則是你登入後期望的初始位置

![enter image description here](images/publishOverSsh/task_ssh_setting.png)
