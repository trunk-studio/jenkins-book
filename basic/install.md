![enter image description here](https://lh3.googleusercontent.com/-vZ7C1C_7fUE/VUCZVwU6rpI/AAAAAAAAP9Q/zSCXlYLE5eQ/s0/jenkins-stickers.png)

ubuntu install jenkins & setting
--------------------------------

openjdk-7-jre and openjdk-7-jdk are suggested.

安裝方式:
---------

-	https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu

```
wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install jenkins
```
