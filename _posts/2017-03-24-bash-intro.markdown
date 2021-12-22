---
layout: post
permalink: /bash-intro/
title:  "Introduction to bash for data analysis"
date:   2017-03-24 15:30:38 -0800
---

# This video covers beginner tips for bash

<iframe width="560" height="315" src="https://www.youtube.com/embed/EMaFdfIlK58" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

The rest of this page is covering the same code as the video so you can copy-paste some of the snippets, and it has a few updates added in 2020.

**Update 2021**: Here is a quick guide to [adapting to ZSH](/adapting-to-zsh/), which is the new default on Macs now. If your computer uses ZSH, skip the command prompt setup below, follow the new guide instead if you want, and just skip to "basic navigation".

## One-time command prompt setup

Start by opening the terminal. (On a Mac, hit command-space and type in terminal.)

I’m going to show you how to navigate around your file system, but first we are going to make a quick change that will make navigating easier (forever).

If you are working on your local computer:

```bash
touch ~/.bash_profile
open ~/.bash_profile
# or if 'open' is not available on your system, use any text editor to edit the file.
```

If you are ssh-ing into a remote machine, use whatever text editor you are comfortable with, such as vim:

```bash
vim ~/.bashrc
```

That should open a text editor, and then you can copy in the following code:

```
function prompt
{
    local BGreen='\e[1;32m'       # Green
    local BIBlue='\e[1;94m'       # Blue
    local GRAY="\[\033[0;37m\]"   # Gray
    local BYellow='\e[1;33m'      # Yellow
    local BLACK="\[\033[0;30m\]"  # Black
    local CYAN='\e[\033[1;36m'    # Cyan
    export PS1="
${BGreen}\u${BGreen}@${BGreen}\h:${BIBlue}\w${BLACK}
$ "
}
prompt
```



Once you have saved that file, either type in
```
source ~/.bash_profile # or ~/.bashrc
```
or just open a new terminal.


You should now see green and blue text that used to be black. The code we added has two advantages:
* it adds color to help orient us, and
* it shows the entire path of where you are instead of only the name of the folder you are in.

## Basic navigation

```
cd ~/Desktop
mkdir my_folder
cd my_folder
cd ..
cd my_folder
mkdir another_folder
cd another_folder
cd ../..
```

## Make and edit a file

```bash
touch my_file.txt
open my_file.txt
# OR try nano if it's available on your system
nano my_file.txt
# OR check out vim if you don't mind a slightly steeper learning curve (but way more power)
vim my_file.txt
```

If you're not ssh-ing but using your local computer, then you can use your favorite text editor like VSCode. I prefer to do quick edits from the command-line using `vim`, but I use VSCode for anything bigger.

In the video I may have mentioned Sublime Text, but since then I've been using VSCode, which I think is even better and completely free.

However you're editing the file, paste in the following:

```
Pikachu	Electric	none
Bulbasaur	Grass	Poison
Charmander	Fire	none
Squirtle	Water	none
Caterpie	Bug	none
Weedle	Bug	Poison
Pidgey	Normal	Flying
Ivysaur	Grass	Poison
Charmeleon	Fire	none
Wartortle	Water	none
Metapod	Bug	none
Kakuna	Bug	Poison
Pidgeotto	Normal	Flying
Venusaur	Grass	Poison
Charizard	Fire	Flying
Blastoise	Water	none
Butterfree	Bug	Flying
Beedrill	Bug	Poison
Pidgeot	Normal	Flying
```

Make sure you save the file, then close it and let’s look at it from the command-line.


## Viewing file contents

There are several ways to look at the contents of a file. These are the ones I use regularly.

Output everything to the terminal:
```
cat my_file.txt
```
Output the first 10 lines (the default) or 5 lines:
```
head my_file.txt
head -n 5 my_file.txt
```
(replace head with tail to get the last lines)

Show the file and close it without clogging up the terminal:
```
less -S my_file.txt
# use arrow keys to move around the file
# type q to quit
# type h to see help menu
# the -S stops it from wrapping long lines.
```

## Data analysis

Let’s count how many Pokémon of each type are on our list here. We are going to build this up step by step using the “|” character called a pipe.

Print everything to the terminal
```
cat my_file.txt
```

Pipe that to `cut` to get the second column
```
cat my_file.txt | cut -f 2
```

### Side note
If you still see the whole file there, then the tabs converted to spaces at some point. If you ever need to convert weird spacing to tabs, use this trick:
```
cat my_file.txt | awk '{$1=$1;print}' OFS='\t' > my_file_with_tabs.txt
# Check that my_file_with_tabs.txt looks right
# Then move it into the place of the first file:
mv my_file_with_tabs.txt my_file.txt
```

### Counting items

Pipe that to uniq -c which consolidates and counts (-c) the rows
```
cat my_file.txt | cut -f 2 | uniq -c 
```

Output:
```
1 Electric
1 Grass
1 Fire
1 Water
2 Bug
1 Normal
1 Grass
1 Fire
1 Water
2 Bug
1 Normal
1 Grass
1 Fire
1 Water
2 Bug
1 Normal
```

Notice that some of these types are listed more than once. This is because uniq can only consolidate entries that are right after each other.

We can fix this by first sorting the list
```
cat my_file.txt | cut -f 2 | sort
```
And now we’ll pipe the sorted output to 
```
uniq -c
cat my_file.txt | cut -f 2 | sort | uniq -c
```

Output:
```
6 Bug
1 Electric
3 Fire
3 Grass
3 Normal
3 Water
```

For clarity we can sort this output by the counts
```
cat my_file.txt | cut -f 2 | sort | uniq -c | sort -k1,1nr
```
Sort works alphabetically on the whole line if there are no arguments. Here I am saying I want to sort -k1,1: only columns 1 through 1 (meaning just the first column), -n: numerically, -r reverse (highest number at the top).
Output:
```
   6 Bug
   3 Fire
   3 Grass
   3 Normal
   3 Water
   1 Electric
```
Sticking together -n and -r with the -k1,1 is a pattern that allows you to sort by multiple columns in different ways. A great example in bioinformatics is how bedtools asks you to sort .bed files first by chromosome (column 1) and then within each chromosome group, increasing numerically by position (column 2): `sort -k1,1 -k2,2n`.


## Ta-daa

By stringing a few commands together you can do all sorts of good stuff in bash, like counting categories of Pokémon.


Wrapping up for this time, I want to leave you with a few shortcuts and general tips:
1. Get out of trouble with control-c. Use control-c to stop running a program or get out when it’s not responding because you accidentally opened a quote and didn’t finish it or something.
2. Use control-a to jump to the beginning of a line you are typing
3. Use control-e to jump to the end of a line you are typing
4. Tab to complete, tab twice to see options when there are multiple
5. See your history of commands: `history`
6. Where to get help: Most programs will let you type --help to get a quick help printout, e.g. `sort --help`. You can also type in `man` before a program’s name to get the manual for it, e.g. `man sort`.

Of course Google is great when you have a specific thing you are trying to do; look for Stack Overflow results to get the best quick answers.
