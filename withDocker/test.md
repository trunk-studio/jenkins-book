測試專案使用 docker
-------------------

複製 task/[test](../task/test)

將執行 bash 指令修正為

```
docker-compose up -d mysql
docker-compose run --rm build
docker-compose run --rm test
```
