預覽專案使用 docker
-------------------

複製 task/[preview](../task/preview)

將執行 bash 指令修正為

```
docker-compose up -d mysql
docker-compose kill web
docker-compose up -d web
```
