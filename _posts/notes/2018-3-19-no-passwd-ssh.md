---
layout: post
title: No passwd ssh
categories: linux
---


#### one line

```
    ssh-copy-id -i ~/.ssh/id_rsa.pub <romte_ip>
```


### raw

+ Generate keypair

```
ssh-keygen
```

+ Scp rsa.pub to remote-server

```
scp ~/.ssh/id_rsa.pub admin@server.io
```

+ Authority

```
chmod 600 ~/.ssh/authorized_keys
```
