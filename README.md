# mysql-schemacrawler-docker

Generate the ER diagram of tables created in mysql 5.6.

# Requirement

docker-compose
graphviz

# Commands (MacOS) 

```
docker-compose pull
docker-compose build

docker run --name mysqlschemacrawlerdocker_mysql_1 -e MYSQL_ROOT_PASSWORD=mysql -d -p 3306:3306 mysql:5.6

# create test tables
mysql -h$(docker-machine ip default) -P3306 -uroot -pmysql < ./create-tables.ddl

# generate a dot file
docker run -v $(pwd):/output \
  --link mysqlschemacrawlerdocker_mysql_1:db \
  --rm mysqlschemacrawlerdocker_schemacrawler \
  -url="jdbc:mysql://db:3306/test" \
  -user=root \
  -password=mysql \
  -infolevel=maximum \
  -loglevel=CONFIG \
  -command=graph \
  --outputformat=dot \
  --outputfile=/output/database.dot

# generate pdf from dot file. use osage to make diagram layout better.
osage -Tpdf -o database.dot.pdf database.dot
```

# Reference

[https://hub.docker.com/r/symfoni/schemacrawler/](https://hub.docker.com/r/symfoni/schemacrawler/)

