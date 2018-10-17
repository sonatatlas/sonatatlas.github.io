---
layout: post
categories: git
title: Clone file inside git repo
---

### Base on sparse clone

```shell
mkdir sparse
cd sparse
git init
git remote add origin https://github.com/user/repo.git
git config core.sparsecheckout true
echo "app" >> .git/info/sparse-checkout
git pull origin master
```
