---
layout: post
title: Emacs Without ~
categories: emacs
---

__`e ~/.emacs` oneline config:__

```
(setq make-backup-files nil)
```

__or__

```
(setq backup-directory-alist '(("." . "~/.emacs.d/backup"))
  backup-by-copying t    ; Don't delink hardlinks
  version-control t      ; Use version numbers on backups
  delete-old-versions t  ; Automatically delete excess backups
  kept-new-versions 20   ; how many of the newest versions to keep
  kept-old-versions 5    ; and how many of the old
  )
```

__or redirt the directory(recommend):__

```
;; Put autosave files (ie #foo#) and backup files (ie foo~) in ~/.emacs.d/.
; create the autosave dir if necessary, since emacs won't.
(make-directory "~/.emacs.d/autosaves/" t)
(make-directory "~/.emacs.d/backups/" t)
; put files
(custom-set-variables
  '(auto-save-file-name-transforms '((".*" "~/.emacs.d/autosaves/" t)))
  '(backup-directory-alist '((".*" . "~/.emacs.d/backups/"))))
```
