docker 執行環境安裝
===================

docker install on ubuntu
------------------------

```
sudo apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
sudo add-apt-repository "deb https://apt.dockerproject.org/repo ubuntu-$(lsb_release -s -c) main"
sudo apt-get update
sudo apt-get install docker-engine
sudo docker run hello-world
sudo usermod -aG docker jenkins
```

docker-compose install on ubuntu
--------------------------------

下述指令請用 `root` 執行

```
curl -L https://github.com/docker/compose/releases/download/1.4.2/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

建立 check jenkins environment docker task
------------------------------------------

指令如下

```
id
docker -v
docker-compose -v
docker ps
docker login -e smlsun.xie@gmail.com -p jenkins4ever -u trunkworkshopjenkins
```

範例結果如下

```
uid=116(jenkins) gid=125(jenkins) groups=125(jenkins),998(docker)
Docker version 1.8.3, build f4bf5c7
docker-compose version: 1.4.2
CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS              PORTS                    NAMES
a71fb8e3990f        miiixr/picklete_env   "/bin/bash -l -c 'npm"   16 hours ago        Up 2 minutes        0.0.0.0:1337->1337/tcp   nodejsSample
dc968421b7dc        dgraziotin/mysql      "/run.sh"                16 hours ago        Up 2 minutes        0.0.0.0:3306->3306/tcp   mysql
Finished: SUCCESS
```
