---
layout: post
permalink: /getting-started-bioinformatics/
title:  "Getting started with bioinformatics"
date:   2017-04-17 15:30:38 -0800
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/A8vjlqUOniY" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## A practical introduction to doing bioinformatics research

Bioinformatics is a huge field and nobody can be an expert on everything, but here are a few recommendations for how to get started learning and doing bioinformatics. I also share my favorite podcasts and online genomics communities.

I got this question from a viewer (paraphrased):

> I am a first year PhD student in a wet lab, where I am the only one doing bioinformatics. I started learning R after your first video, but I feel that I need more guidance on how to get started with bioinformatics.

Here is the path that I would recommend for beginners in bioinformatics:

## 1. Start with a foundation in Python/R and bash

In Python/R: Just get to the point where you can read in data and run a statistical test.

In Bash: Be able to navigate around directories, open files, and run a program (like sort, uniq, or wc) and output the result to a file. Check out my intro video on bash for quick tutorial on getting started on the command-line.

## 2. Do a small project
Start with a simple project where you take some data, do some analysis of it, and present the results with plots in a powerpoint presentation or equivalent.

You can use publicly available data. A good source is the UCSC genome browser, where you can use the Table Browser to download csv files.

It is even better if you have data from your own project or from your lab that you can play with, which will make your results more interesting to everyone around you, and more publishable!

Start by actually understanding where the data comes from, why it was generated, and what kinds of biological questions you may be able to answer with it.

A few ideas for what to do with data: look into statistical tests to run, check out machine learning techniques like PCA, look for correlations, or just start plotting to see if there are any patterns you want to investigate further.

Google as you go!

If you get completely stuck and google doesn’t answer your questions after several tries, you can ask coding questions on Stack Overflow or bioinformatics questions on Biostars.

## 3. Occasionally do tool safaris

Make sure you are aware of the commonly used tools for your field, which means you know their names and their main purpose. You can always learn more when you need them. Here is an example.

There is a tool called [bedtools](https://bedtools.readthedocs.io/) that is super useful for comparing sets of genomic intervals, called bed files. If you are asking a question like how many of these variants we found overlap with lincRNA’s, bedtools will give you an answer. Before I knew bedtools existed, there were a few times that I had questions like that and wrote whole python scripts to do the comparison.

If I had known bedtools existed, even if I had no idea how to use it yet, I would just have googled it, figured out how to use it, and solved my problem much faster. I didn’t need to spend weeks learning how to use every tool in the NGS field, but if I had done a couple of searches on Google for useful bioinformatics tools, I would have been aware enough to go back and find it later.

## 4. Build tools to fill gaps as they come up in your research
If you want to do bioinformatics as a career, I would recommend over time finding places where there are gaps in the tools available and filling it in by writing a tool of your own to solve the problem. Writing tools is fun and puts you in a place where finding a job is easier, especially in industry.

Making a tool is as easy as building an R package or turning a python script into a command-line program using argparse, but it can also be as complicated as web applications. For any tool you are building, consider starting with a minimum viable product. You will naturally find gaps as you are doing analysis, so just focus on solving the problems as they come up in the projects you do.

## Productive entertainment

Look for podcasts, blogs, or people to follow on Twitter. For podcasts, I recommend following [Mendelspod](https://podcasts.apple.com/us/podcast/mendelspod-podcast/id988565102) for news and stories, especially around biotechologies and the future. I really like the interviews on [The Genomics Life podcast](https://podcasts.apple.com/us/podcast/the-genomics-life/id1500134545), and not just because the host Kelly Moffat is a good friend of mine. I also like the Effort Report for discussions on life and career as an academic, even though I'm not an academic myself anymore :)

There are also relevant subreddits, like [reddit.com/r/genomics](http://reddit.com/r/genomics) and [reddit.com/r/bioinformatics](http://reddit.com/r/bioinformatics).

## And for fun:
Check out the [PhD Comics](http://phdcomics.com/) if you haven’t already. I read through all of them right when I was applying to graduate schools and I thought, "hey graduate school sounds really hard but I think I can do it".

The [XKCD](https://xkcd.com/) is also an awesome comic, more related to programming/math/and generally geeky stuff but it has a great sense of humor.

And there is a great dystopian movie called [Gattaca](https://en.wikipedia.org/wiki/Gattaca) that gives some perspective on what the social impact may be of the work we are doing right now to understand the human genome.

