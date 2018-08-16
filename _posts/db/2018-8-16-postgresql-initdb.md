---
layout: post
categories: db
title: Postgresql Starting
---


#### Preparation


```
initdb -D /usr/local/pgsql/data

pg_ctl -D /usr/local/pgsql/data initdb

```


#### Starting the Database Server

+ Default Start

```
postgres -D /usr/local/pgsql/data

postgres -D /usr/local/pgsql/data > logfile 2>&1 &

```  



+ With logfile

```
pg_ctl start -l logfile

su postgres -c 'pg_ctl start -D /usr/local/pgsql/data -l serverlog'

/usr/local/pgsql/bin/pg_ctl start -l logfile -D /usr/local/pgsql/data

```
