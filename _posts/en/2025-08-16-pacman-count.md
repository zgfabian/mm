---
title: "Counting how many arch packages do you use"
layout: single
lang: en
categories: Linux
tags: [pacman, wc, CLI]
---

How many arch package have you installed?

`pacman -Q | wc -l` (all installed)
`pacman -Qe | wc -l` (explicitly installed)

Does the number of installed arch linux packages mean anything in terms of performance? No, not at all. The packages themselves just use some space on your drive.

r/arch
