---
layout: post
categories: git
title: Change Default Lang of Git Proj
---

sometimes git makes mistakes on default language of our project.
I upload my `emacs.d` just now, and it appears javascript... lol

edit `./gitattributes`
```
*.js linguist-language= Emacs Lisp
```

done
