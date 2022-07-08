---
title:  "Checking for and removing ^M line endings from a file"
permalink: /carrot-m/
layout: post
---

## How to look for ^M line endings

* Open in `vim`. Note that `less` and `cat` did not show these, at least on my computer.

## Ways to remove the ^M line endings

* In vim: `:%s/\r$//g`
* On the command line (easier to automate and reproduce): `sed 's/\r$//g' original_file.txt > fixed_file.txt`

Interestingly this particular file, when I `cat` it, shows a highlighted % sign on the very last line, which was the only line that didn't have the ^M showing up in vim. This didn't seem to bother Circa though.
