---
layout: post
title: No passwd ssh
categories: linux
---

+ Generate keypair

```
ssh-keygen -t rsa -P
```

+ Scp rsa.pub to remote-server

```
scp ~/.ssh/id_rsa.pub admin@server.io
```

+ Authority

```
chmod 600 ~/.ssh/authorized_keys
```
