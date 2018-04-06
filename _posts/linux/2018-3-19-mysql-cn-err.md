---
layout: post
title: MySQL ZH ERR
categories: linux
---

Migrate project to EN environment, mysql err.


+ show character_set

```sql
show variables like'character_set_%';
```

+ alter database charset

```sql
alter database <yourdatabase> character set utf8;
```

+ set mysql charset

```sql
SET character_set_connection = utf8 ;
SET character_set_server = utf8 ;
...
```

+ install ZH environment in system
