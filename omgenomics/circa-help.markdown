---
layout: page
# Add a `title` to make this show up in the header
permalink: /circa/help
description: Circa Tutorials and FAQ
---

## Tutorial videos

<iframe src="https://www.youtube.com/embed/iIlGQcRtMzY?showinfo=0" width="560" height="315" allowfullscreen="allowfullscreen"></iframe>

<iframe src="https://www.youtube.com/embed/cKlJDhucul8?rel=0&amp;showinfo=0" width="560" height="315" allowfullscreen="allowfullscreen"></iframe>

<iframe src="https://www.youtube.com/embed/Maxaz637rP4?rel=0&amp;showinfo=0" width="560" height="315" allowfullscreen="allowfullscreen"></iframe>

<iframe src="https://www.youtube.com/embed/2Gs4-xXn83c?rel=0&amp;showinfo=0" width="560" height="315" allowfullscreen="allowfullscreen"></iframe>

Don't forget to read the [Input file guide](/circa/input-file-formats) too!

## FAQ

### What operating systems can I run Circa on?
Mac, Windows, and Linux.

#### How do I install Circa on Linux?
You will be able to download Circa as an AppImage. In order to run Circa, you download the AppImage, right click on it, choose Properties, go to the Permissions tab, and click the make executable checkbox. Now you can double-click it to open.

### Is Circa built using Circos?
Nope, Circa is made completely from scratch using D3.js. This makes Circa run much faster compared to constantly calling some Perl code every time you make a change to the plot.

### How do I cite Circa?
You can mention Circa in the methods of your paper by saying something like “circos plot created with Circa (http://omgenomics.com/circa).”

### Can I plot non-genomic data in Circa?
Circa plots all data with respect to chromosomes and positions within the chromosomes. It works for any genomic data where you have that chromosome and position information. For non-genomic data, a circos plot is usually not an ideal way to show the data. Consider making regular cartesian plots of non-genomic data instead, for instance using ggplot in R.

### What types of data can I plot with Circa?
Anything you can put into a CSV, tab-separated, or VCF text file of less than 10 MB. If you have bigger data, try to consolidate it first into a smaller file. You can test the size of a file on the command-line using “du -skh my_file.csv” See the file formats guide for more information.

### How can I save my plot as an image?
To save your plot in Circa as an image, just click on File in the navigation menu, go to Save as image, and click on either PNG or SVG. PNG is a regular image file that you can put into your paper or presentations. SVG stands for Scalable Vector Graphics, which is perfect for final submission to a journal when they want vector formats instead of raster. SVG makes your image look crisp in print and allows readers to zoom into the plot infinitely without it ever looking pixelated.

### Why can’t I select a certain column in my file to be the position, size, or y?
Position, size, and y must be numbers. If that column contains any data points that are not numbers, then the column cannot be used as a numeric variable. Check to make sure that column doesn’t have any NA values or other non-numeric content.
You can easily filter these out in Excel or on the command-line.

### What if I only have one chromosome?
You still need a genome file with a header and a single line:
```
chromosome,size
Ecoli,1234567
```
The “chromosome” name can also be your species name, just make sure it appears the same way across all your datasets, so for bacterial genomes you may want to add a column to all your datasets that have some common chromosome name, and you can always hide that one boring chromosome label once you make the plot.
See the [input data guide](/circa/input-file-formats) for an in-depth explanation of the genome file and how to create one.

### Why do I get an error that some points are being ignored?
Data can only be plotted if the chromosome names match those in the genome file you initialized your circos plot with. Make sure those chromosomes affected have the exact same names as in the circos plot labels (see note on “chr” prefixes below). If only a few points are ignored, it is usually because their given positions are outside the size of the chromosome, pointing to inconsistencies between the chosen reference genome (chromosome sizes) and the data you are plotting.

### Why does Circa ask about removing “chr” prefixes?
Circa will ask you whether you want to remove “chr” prefixes from your datasets, which is recommended to make the labels look nicer and to remove inconsistencies in naming conventions across files. If you choose to leave in the “chr” prefix by hitting “Cancel” when Circa asks about it, make sure all of your datasets also have the “chr” prefix or their points will be ignored.

### How can I stop text in the text layer from overlapping?
To stop the text from overlapping you could decrease the font size of the Text layer, or you can manually move around the labels in Illustrator or Inkscape after exporting the SVG from Circa.

### What is included with Circa?

When you buy Circa, you will get immediate access to download **Circa for Mac, Windows, and Linux** operating systems. You will also get a **Starter Pack** of example input files and case studies to experiment with.


**Any questions not answered here, the tutorial videos above, or in the [input data guide](/circa/input-file-formats)? Then email me at maria@omgenomics.com.**

------

[![Click here to buy Circa](/assets/circa/buy-circa.png)](https://gum.co/circa)
