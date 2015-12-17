![enter image description here](https://lh3.googleusercontent.com/-vZ7C1C_7fUE/VUCZVwU6rpI/AAAAAAAAP9Q/zSCXlYLE5eQ/s0/jenkins-stickers.png)

Jenkins 可以在 Windows、Linux 或 Mac OS X 環境執行，一般來說我們會盡可能選擇跟 Production / Testing 伺服器接近的環境來運行。

ubuntu install jenkins & setting
--------------------------------

安裝 Java 軟體
---------------

建議使用 JDK 1.7 以上版本。

```
sudo apt-get update
sudo apt-get install openjdk-7-jdk
```

安裝 Jenkins 軟體
-----------------

參考 Jenkins 官方的 Ubuntu Linux [安裝說明](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu)

```
wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install jenkins
```
