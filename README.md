# docker-isucon-go-local

local で isucon-go を構築するための Docker

```
$ docker-compose exec db bash
# pwd
/home
# ./db/init.sh
# mysql < setToInsertData.txt ## いらないかも
# zcat  zcat db/init.sql.gz | mysql isubata
```
