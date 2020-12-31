---
layout: post
permalink: /data-wrangling/
title:  "Intro to data wrangling for bioinformatics"
date:   2017-05-09 15:30:38 -0800
---

Data wrangling is a very practical skill that you will definitely need in your data science or bioinformatics work. It is all about getting data into the right format so it can be used by various downstream tools, plotted visually, or analyzed statistically.

<iframe width="525" height="315" src="https://www.youtube.com/embed/OnM3sGNMJTE" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Top tools

## Text editor like Sublime text or VSCode

You can edit multiple lines at once in Sublime Text by holding down the option key while dragging across the lines. In the video I use this to select all of the “chr” prefixes and delete them, and there are many other ways to use this powerful text editor for some pretty extensive data wrangling. The video mentions Sublime Text, but I have since switched to [VSCode](https://code.visualstudio.com/), which has similar features. Either works well for this though!

## Excel has some decent data wrangling features that you can take advantage of

With GUI wizards and lots of guided tools and explanations, Excel can be used for some of the more basic data wrangling tasks. If you are already working with Excel, it is more convenient to fix a few issues without exporting your data first, and more things may be possible than you think. By Googling for how to split columns by a delimiter, I found out Excel has a neat little tool which does exactly that.

## Awk is a powerful and flexible command-line language

There is a lot to say about awk since it is a full programming language in itself, even though we usually reserve it for one-liners. You can filter rows, change values, do calculations, and completely reformat a data file with awk. Here I will just show you how to easily filter the rows based on their content in each column.
If you need an introduction or a refresher on the command-line, check out this [bash introduction](/bash-intro/) first.

A full explanation is in the video, but here is the snippet of code.
```
awk '$7>=99.9 && $12=="chrX"' hg19_to_GRCh38.txt > hg19_to_GRCh38_filtered.txt
```
This checks that column 7 ($7) has a value greater than or equal to 99.9 AND (&&) that column 12 ($12) equals (==) “chrX”. Don’t forget to put awk at the beginning and encase the rest of the statement in single quotes (‘). The file name goes last, and then we used “>” to write the resulting output to a new file. You have to output to a different file, never to the same one, because the input file is being read gradually and prints gradually to the output, so if you read and write on the same file at the same time it will have issues.
Here are a few other command-line programs you can look into for specific problems you encounter:

* grep for search
* sort for sorting
* uniq for consolidating redundant rows
* sed for find/replace

## That was a small taste of data wrangling with different tools
Data wrangling is not an easy thing to learn or to teach because it is different every time. It is something you will learn as you go. Every dataset has a unique set of issues you have to deal with, but if you are just familiar with a few tools that do similar things to what you are trying to accomplish, you can always Google the rest.