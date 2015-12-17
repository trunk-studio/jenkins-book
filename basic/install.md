![enter image description here](https://lh3.googleusercontent.com/-vZ7C1C_7fUE/VUCZVwU6rpI/AAAAAAAAP9Q/zSCXlYLE5eQ/s0/jenkins-stickers.png)

Jenkins 可以在 Windows、Linux 或 Mac OS X 環境執行，一般來說我們會盡可能選擇跟 Production / Testing 伺服器接近的環境來運行。

本書範例皆以 Ubuntu Linux 演示
-------------------------------

因為 Ubuntu Linux 相容多數 Open Source 軟體，也被用於許多 Production Server 環境，因此使用 Ubuntu Linux 作為 Jenkins 入門的系統，可以避免很多干擾學習的問題發生。 

建議搭配 VirtualBox 虛擬機器使用 Ubuntu Linux + Jenkins，我們也為學習者提供已安裝設定完成的 VirtualBox Image，請向課程主辦單位索取。

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
