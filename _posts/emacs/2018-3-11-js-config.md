---
layout: post
categories: emacs
title: Set js as jsx in web-mode
---

indent is a big problem while developing. 
I used to write jsx without html indent... 
what a tough time, I can't look back

# add js file to web-mode-alit

```el
;; auto use web-mode to .js
(add-to-list 'auto-mode-alist '("\\.js\\'" . web-mode))
```

# match js to jsx

```el

;; use js as jsx
(setq web-mode-content-types-alist
'(("jsx" . "\\.js[x]?\\'")))

```

# in the same way, ts config

```el
;; auto use web-mode to ts
(add-to-list 'auto-mode-alist '("\\.js\\'" . web-mode)

;; use ts as tsx
(setq web-mode-content-types-alist
'(("jsx" . "\\.js[x]?\\'")))
```
# keep ts and js in jsx formate

```el
(setq web-mode-content-types-alist
'(("jsx" . "\\.[jt]s[x]?\\'")))
```
