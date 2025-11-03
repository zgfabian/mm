---
title: "Emacs dired ricing"
categories: emacs
tags: dired
lang: en
---

# Table of Contents

1.  [Dired config in Emacs](#orgf9e8abc)
    1.  [Dual-panes and interactions (dwim copy, move) between the panes](#org48f62cf)
    2.  [Hide | show file properties](#org2db23d5)
    3.  [Hide | show dotfiles](#org0092bc9)
    4.  [Icons with all-the-icons](#org9e785c4)
2.  [Excerpt from `init.el`:](#orgaa2b545)



<a id="orgf9e8abc"></a>

# Dired config in Emacs

`Dired` is a file manager in Emacs  .
My setup has the following features:


<a id="org48f62cf"></a>

## Dual-panes and interactions ([dwim](https://en.wikipedia.org/wiki/DWIM) copy, move) between the panes

I am using a convenience function (`(dual-dired)`) binded to `C-c d` combo.


<a id="org2db23d5"></a>

## Hide | show file properties

with pressing `)` key, which is a default.


<a id="org0092bc9"></a>

## Hide | show dotfiles

with a custom `C-.` binding.


<a id="org9e785c4"></a>

## Icons with all-the-icons


<a id="orgaa2b545"></a>

# Excerpt from `init.el`:
```emacs-lisp
      (use-package dired
        :config
        ;; stop proliferating buffers
        (setq dired-kill-when-opening-new-dired-buffer t)
        ;; default target other window for file operations (copy, move)
        (setq dired-dwim-target t)
        ;; confirm recursive deletion or copy
        ;; 'top means ask every time
        ;; 'always means no asking
        (setq dired-recursive-copies 'top)
        (setq dired-recursive-deletes 'top)
        :hook
        (dired-mode . dired-hide-details-mode) ;;
        (dired.mode . dired-omit-mode) ;; hide dotfiles, etc
        )

      (setq dired-omit-files "^\\...+$")
      (global-set-key (kbd "C-.") 'dired-omit-mode)

      (use-package all-the-icons-dired
        ;; :ensure t
        :config
        (setq all-the-icons-scale-factor 1)
        (setq all-the-icons-dired-monochrome nil)
        :hook
        (dired-mode . all-the-icons-dired-mode)
        )

      (defun dual-dired ()
      "Open 2 dired buffers side by side."
      (interactive)
      (let ((original-window (selected-window)))
        (dired "~")
        (split-window-right)
        (other-window 1)
        (dired "~")
        (select-window original-window)))
    ;; Bind the function to a key combination
    (keymap-global-set "C-c d" 'dual-dired)
```
