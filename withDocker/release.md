發布專案使用 docker
-------------------

建置 image
----------

複製 task/[release](../task/release)

```
docker build --no-cache -t trunkworkshop/nodejssample .
docker push trunkworkshop/nodejssample:latest

docker rm -f sample
docker run -d -p 3333:1337 --link mysql --name sample trunkworkshop/nodejssample
```
