---
layout: post
permalink: /excel/
title:  "Should biologists use Excel?"
date:   2017-04-10 15:30:38 -0800
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/7Tyf3mpQa-c" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Excel is a commonly used tool for analyzing data in biology, but it has a bad habit of converting gene names to dates. Here is how you can fix the gene-to-date problem and continue using Excel productively in your research.

## Is Excel a useful tool for analyzing data in biology/bioinformatics?

I had a chat with Robert Aboukhalil about whether Excel should be used for analyzing biological data. He has a PhD in bioinformatics from Cold Spring Harbor Laboratory, where we studied at the same time. Now he works as a bioinformatics software engineer in industry. He uses cloud computing and web development to create tools that help biologists analyze sequencing data.

Robert and I agree that we should all be pragmatic about our research and not listen to people who say that you should never use Excel for biology.

We both use Excel (or Google Slides) for some things like manual curation and entering measurements. And then we switch to R, Python, or other languages for working with big data or specialized plotting and statistics.


## Excel converts some gene names to dates
We also discuss how Excel has a problem with some gene names that it thinks are dates.

For instance, it turns OCT4 into October 4th. Since this only happens to a few genes, the literature is littered with supplementary datasets containing these date-formatted genes. The problem is that when you then do downstream analysis, the databases do not match the gene names in their date formats. You might miss important results related to these genes!

Robert talked about a few ways of avoiding this and shared a free app he built for getting around the issue. You can get Oct4th as a command-line tool: `pip install oct4th` or use the web app at https://oct4th.sandbox.bio.

You can catch up with Robert on Twitter at [@RobAboukhalil](https://twitter.com/robaboukhalil) and me at [@MariaNattestad](https://twitter.com/marianattestad).
