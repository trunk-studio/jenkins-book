搭配 docker 使用 Jenkins 協助測試
=================================

docker install on ubuntu
------------------------

```
sudo apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
sudo add-apt-repository "deb https://apt.dockerproject.org/repo ubuntu-$(lsb_release -s -c) main"
sudo apt-get update
sudo apt-get install docker-engine
sudo docker run hello-world

```

docker-compose install on ubuntu
--------------------------------

下述指令請用 `root` 執行

```
curl -L https://github.com/docker/compose/releases/download/1.4.2/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```
