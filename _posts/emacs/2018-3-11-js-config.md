---
layout: post
categories: emacs
title: Set js as jsx in web-mode
---

indent is a big problem while developing. 
I used to write jsx without html indent... 
what a tough time, I can't look back

```el
;; auto use web-mode to .js
(add-to-list 'auto-mode-alist '("\\.js\\'" . web-mode))
(add-to-list 'auto-mode-alist '("\\.ts\\'" . web-mode))

;; use js as jsx
(setq web-mode-content-types-alist
'(("jsx" . "\\.js[x]?\\'")))

;; use ts as tsx
(setq web-mode-content-types-alist
'(("jsx" . "\\.ts[x]?\\'")))
```
