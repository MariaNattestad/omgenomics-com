---
layout: post
permalink: /python-command-line-program/
title:  "How to turn a python script into a command-line program"
date:   2017-05-01 15:30:38 -0800
---

# You can use the argparse package to easily turn a python script into a command-line program

This is an applied example of using `argparse` to build a small command-line program from a python script. I use argparse for every python script I make because working with NGS data, I spend all of my time on the command-line. Making your python scripts into command-line programs makes them much easier to use and lets them fit neatly into a pipeline of other tools.

<iframe width="560" height="315" src="https://www.youtube.com/embed/zi-FIG3efag" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

For quick reference, here is some boilerplate you can copy for your own scripts:

Create a text file (open, nano, vim, or sublime depending on what you have for a text editor) and name it fasta_to_fastq.py
```
#! /usr/bin/env python
import argparse

def run(args):
	filename = args.input # these match the "dest": dest="input"
	output_filename = args.output # from dest="output"
	qual = args.quality_score # default is I

	# Do stuff


def main():
	parser=argparse.ArgumentParser(description="Convert a fastA file to a FastQ file")
	parser.add_argument("-in",help="fasta input file" ,dest="input", type=str, required=True)
	parser.add_argument("-out",help="fastq output filename" ,dest="output", type=str, required=True)
	parser.add_argument("-q",help="Quality score to fill in (since fasta doesn't have quality scores but fastq needs them. Default=I" ,dest="quality_score", type=str, default="I")
	parser.set_defaults(func=run)
	args=parser.parse_args()
	args.func(args)

if __name__=="__main__":
	main()
```
Make the script executable the first time you run it:
```
chmod +x fasta_to_fastq.py

# Then run the script:

# Default quality score:
./fasta_to_fastq.py -in file.fasta -out file.fastq

# Setting a custom quality score:
./fasta_to_fastq.py -in file.fasta -out file.fastq -q G
```

Check out the [documentation for argparse](https://docs.python.org/3/library/argparse.html).

## A real example in bioinformatics

Let’s make a python script that converts fastA to fastQ.
FastA files contain sequence data, while fastQ contains sequence data plus quality scores. Therefore if you have a tool that requires fastQ files and you only have fastA files, you will have to make up the quality scores. Just make sure the quality scores are not actually used by the tool, and if they are, try to recover the original fastQ files.

FastQ files typically contain sequencing data such as raw reads where the quality scores say something about how sure the sequencer is about the base it picked for that specific location. FastA files are more commonly used for storing assemblies, which don’t have any relevant quality scores on a single-base level.

FastA files look like this (sequences shortened):
```
>chr1 additional info
AATGTGTAATTTGAATCAATTTCTATCCTTTTAAAAATACATCATAAAGTGTACTTTTTT
TTAGTTATTAAAGGATTAATTATGGATTGCTAACCAGTTAATATTAAGAGGAAGAAGGAT
```
Each line that starts with a “>” contains the name of the sequence (usually a chromosome or contig from an assembly), and there are many lines of sequence after it.

FastQ files look like this (sequences shortened):
```
@D00777:42:HF5YNBCXX:1:1101:1244:2123 1:N:0:1
NAGGACTGTGTGACTATTGACGTCCTTCCCCGTACGCCGGGCAATAATGTTTATGTTGGTTTCATGGTTTG
+
CGHHIIIIIHGHIHHIHHHHHHIHIHHIIIIIIIIIIIHHIIIHGFHGEFHHIIIEHHEEHIHIIIEHIHH
```
To make the fastA file into a fastQ file, we need to make 4 rows for each “>” in the fastA file.

1. the name from the “>” line in fastA, just starting with “@” instead of “>”
2. sequence (unfolded version of sequence in fastA)
3. +
4. quality scores that we have to make up because they don’t exist in fastA

Using argparse, here is a script that parses the fastA file and outputs it into the output file in fastQ format as it goes. It is streaming, meaning that the input is read, interpreted, and output along the way. This is an alternative to storing the whole input file in memory, such as putting all of its contents into a list, and then outputting all of it at the end when the input file has been read completely through. Streaming input/output (I/O) can only be done when the output doesn’t depend on knowing the contents of the entire file first. There are cases when the entire input must be read into memory and interpreted together, which is usually when we end up running out of memory if the input file is too large. This happens quickly with sequence data. Here we can output the 4 fastQ lines every time we finish reading one sequence in the fastA file, so it is perfect for streaming.

```
#! /usr/bin/env python
import argparse

def run(args):
	qual = args.quality_score
	f = open(args.input)
	fout = open(args.output, "w")
	seq = ""
	for line in f:
		if line[0] == ">":
			if seq != "":
				fout.write(seq + "\n")
				fout.write("+\n")
				fout.write(qual * len(seq) + "\n")
			fout.write("@" + line[1:])
			seq = ""
		else:
			seq += line.strip()
	f.close()

	fout.write(seq + "\n")
	fout.write("+\n")
	fout.write(qual * len(seq) + "\n")
	fout.close()

def main():
	parser=argparse.ArgumentParser(description="Convert a fastA file to a FastQ file")
	parser.add_argument("-in",help="fasta input file" ,dest="input", type=str, required=True)
	parser.add_argument("-out",help="fastq output filename" ,dest="output", type=str, required=True)
	parser.add_argument("-qual",help="Quality score to fill in (since fasta doesn't have quality scores but fastq needs them. Default=I" ,dest="quality_score", type=str, default="I")
	parser.set_defaults(func=run)
	args=parser.parse_args()
	args.func(args)

if __name__=="__main__":
	main()

```
Don’t forget the make the script executable, otherwise it will give you an error about permissions.
```
chmod +x fasta_to_fastq.py
```
## Other argparse features

Argparse can also do other things. A few useful things to be aware of:

* Use a flag to set a variable to true or false:
```
parser.add_argument('--verbose', help="Output updates while program is running", dest="verbose", action='store_true')
```
Then you can start all output messages with checking if verbose is true:
```if args.verbose == true: print "still running"```
* You can actually run different sub-apps with different sets of required parameters.
This is just like with `samtools index` and `samtools view`. The second word tells the script which sub-app to run and which parameter set it needs to look for. Check the [argparse documentation](https://docs.python.org/3/library/argparse.html) for the specifics.
