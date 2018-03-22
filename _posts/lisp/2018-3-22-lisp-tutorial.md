---
layout: post
categories: lisp
title: Lisp Tutorial
---

## Basic

__command__

```
setq
defun
defmacro
defvar
```

__print__

```lisp
(write-line "hello,world") ;; write-line requires str
(print "hello,world") ;;
(setq str "hello,world") 
(print str) ;; single prop
(write str)
(format str)

```

__macro__

```lisp
(defmacro setTo10(num)
    (setq num 10)(print num))
(setq x 25)(print x)(setTo10 x)

```

__var__

```lisp
;;global
(defvar x 12)
(write x)

;;part
(let 1)
```
