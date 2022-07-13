---
title:  "Capturing both stdout and stderr together in a log file"
permalink: /capturing-logs/
layout: post
---

## Write a small program that writes to both stdout and stderr:

```bash
vim mini_program

# file contents:
echo "1 -- This is normal output"
echo "2 -- This is an error" >&2
echo "3 -- This is normal output"
echo "4 -- This is an error " >&2
# end file contents

chmod +x mini_program
```

Now let's use that to demonstrate what happens when you capture logs in different ways.


## No log capture:

```bash
./mini_program
    1 -- This is normal output
    2 -- This is an error
    3 -- This is normal output
    4 -- This is an error
```

## Using tee without manipulating streams:

```bash
./mini_program | tee raw_tee.log
    1 -- This is normal output
    2 -- This is an error
    3 -- This is normal output
    4 -- This is an error

cat raw_tee.log
    1 -- This is normal output
    3 -- This is normal output
```

By default the pipe just takes the stdout, while stderr is shown on the command line. This is usually what you want at least for smaller programs like `grep`, `sed`, `cut`, etc., so you notice the errors right away instead of piping the error message itself to the next program in a series of pipes, e.g. `cat my_file.txt | grep "error" | cut -f 2 | sort | uniq -c`.

## Getting both stdout and stderr

```bash
./mini_program 2>&1 | tee stdout_plus_stderr.log
    1 -- This is normal output
    2 -- This is an error
    3 -- This is normal output
    4 -- This is an error

cat stdout_plus_stderr.log
    1 -- This is normal output
    2 -- This is an error
    3 -- This is normal output
    4 -- This is an error
```

This is what we want for longer-running tools like in bioinformatics where the iteration time is much longer, there can easily be multiple error messages, and we want to see the output and errors interleaved so we can tell when during the program's execution the problem actually occurs. In short, we just want to capture everything we can to the logs to leave all our options open for what information we want.
