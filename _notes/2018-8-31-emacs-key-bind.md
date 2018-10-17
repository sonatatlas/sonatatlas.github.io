---
layout: post
title: Emacs kbd
categories: emacs
---


+ 将 KEY 映射到另一个 KEY

```elisp
(define-key key-translation-map (kbd "your-key") (kbd "target-key"))
```

+ 函数绑定

```elisp
(define-key some-minor-mode-map (kbd "your-key") 'your-command)
```

+ mode 下绑定

```elisp
;; set
(local-set-key (kbd "your-key") 'your-command)
(add-hook 'some-major-mode-hook '(lambda () (local-set-key ...)))
;; unset
(local-unset-key (kbd "your-key")
```

+ Global set

```elisp
(global-set-key (kbd "your-key") 'your-command)
```
