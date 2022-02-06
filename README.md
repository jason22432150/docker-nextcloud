# docker-nextcloud
Use docker-compose create a complete docker nextcloud container

``` sh
git clone https://github.com/jason22432150/docker-nextcloud.git
mv docker-nextcloud/ nextcloud/
cd nextcloud
docker-compose up -d
```

This is docker-comporse.yml
```yml
version: '2'

volumes:
  nextcloud:
  db:

services:
  db:
    image: mariadb
    container_name: cloudnext-db
    restart: always
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW --innodb-file-per-table=1 --skip-innodb-read-only-compressed
    volumes:
      - /mnt:/mnt
      - db:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=
      - MYSQL_PASSWORD=
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud

  app:
    image: nextcloud
    container_name: cloudnext
    restart: always
    ports:
      - 4101:80
    links:
      - db
    volumes:
      - /mnt:/mnt
      - nextcloud:/var/www/html
    environment:
      - MYSQL_PASSWORD=
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_HOST=db
```

Then you can go 

http://[yourIP]:4101
