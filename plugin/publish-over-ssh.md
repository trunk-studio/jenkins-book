# Publish over SSH 

使用時機：

1. 專案建置完成後需要傳輸到 production 機器時
2. 每日建置完成後需要傳到別台機器進行備份時
3. 檔案傳輸完成後，需要透過遠端機器進行後續指令執行時

## 使用前準備

1. 可在目標機器建立 jenkins user
2. 建立 ssh key



-	su jenkins

	-	generate ssh key
		-	ssh-keygen -t rsa
	-	add public key to server user's authorized_keys
		-	cat ~/.ssh/id_rsa.pub >>~/.ssh/authorized_keys

-	Jenkins SSH Key(private key): [paste key generated at the above step]

-	SSH Server Name: [self pick]

-	Hostname(ip): [self pick](ex: 45.33.83.46)

-	Username: jenkins

-	Remote Directory: [self pick](ex: /srv/www/zuru)

-	remember to 'save' or 'apply'

s![enter image description here](https://lh3.googleusercontent.com/-Z2_W6JPYXxY/VUCZt5X_1II/AAAAAAAAP9o/TxTOnC6b_8o/s0/Screen+Shot+2015-04-22+at+5.32.14+PM.png)

![enter image description here](https://lh3.googleusercontent.com/-N3aFi4lkTsE/VUCZyk4uloI/AAAAAAAAP90/CTGgH6-X1R4/s0/Screen+Shot+2015-04-22+at+5.35.10+PM.png)
