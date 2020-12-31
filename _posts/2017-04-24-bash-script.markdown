---
layout: post
permalink: /bash-script/
title:  "How to write a bash script"
date:   2017-04-24 15:30:38 -0800
---

Writing a bash script is important for setting up pipelines to process data or run a series of different tools. It also makes your results more reproducible, so you can keep track of what you did and make sure you don’t miss a step next time you are repeating the analysis.

This video (and the text version here) shows how to make a simple bash script that takes an input value and another optional input value from the user.

This video assumes you know how to find the command-line/terminal on your computer and edit a simple text file. If you don't know these basics, you can catch up with this [quick bash intro](/bash-intro/).

<iframe width="560" height="315" src="https://www.youtube.com/embed/F-gskSl4pwQ" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Open a new file:
```
nano myscript
```
You can just use your favorite text editor, but `nano` was the one I found easiest when I was starting. I now use `vim` when editing remotely and `VSCode` when editing locally.

## Write the shebang line:
```
#!/usr/bin/env bash
```
This tells the system what program to use to run the code, in this case it should look for a program called bash in the computer’s environment and use that to interpret the code we are writing here.
Note: There are several options for shebang lines, but this one is most likely to work across Linux and Unix systems. See this Stack Overflow discussion for details.

## Write the script contents:
Let’s work with a simple example:
```
echo "HELLO!"
```
“echo” just means print onto the screen in bash.

## Make the script executable
```
chmod +x myscript
```
This is where you tell the system that this is a script and not just a data file, and that you want to be able to run it as software.

## Run the script
```
./myscript
# This should print HELLO!
```
The ./ means that the script is in the same directory. If you go into another directory, you have to specify the relative or whole path to the script, like ~/Desktop/myscript if it is on the desktop. Alternatively, you can make the script globally available by putting it in /usr/local/bin/. What I did is create a bin at ~/bin that contains only my own scripts, added that to my PATH, and then create a symbolic link of each new script into ~/bin/. But that can be the topic of another video.

## Add an input variable
```
#!/usr/bin/env bash
NAME=${1?Error: no name given}
```
If your script needs to take user input, such as a filename, this is how you do it.

## Now run it:

```
# Without the required parameter:
$ ./myscript
./myscript: line 2: 1: Error: no name given

# With the required parameter:
$ ./myscript Tom
HELLO! Tom
```

## Add an optional input variable
```
#!/usr/bin/env bash
NAME=${1?Error: no name given}
NAME2=${2:-friend}
echo "HELLO! $NAME and $NAME2"
```
Instead of throwing an error if there is no input, we are giving a default value. This is a very common thing to do and allows you to pick some sane defaults for your pipeline.

## Now run it again:
```
# With one name:
$ ./myscript Tom
HELLO! Tom and friend

# With two names:
$ ./myscript Tom Jerry
HELLO! Tom and Jerry
```

## Conclusion
There are other ways to deal with user input, but this is a good start.

I hope that gets you going with creating your own command-line scripts.

If you have any questions, you can leave a comment on youtube and I will answer them there.
