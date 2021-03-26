# SI 335 Project: Wrong Name

## Overview

Every year, millions of babies are born in the U.S., and one of the
first responsibilities of the parents is to choose a name. Specifically,
we are focusing on the *first names* in this project.

Unfortunately, names are easy to mis-spell, especially if there are
multiple common spellings for (nearly) the same name.
The misspelability of a name X is a score, carefully defined below, which
describes the likelihood of encountering a name which is less popular
than X, but whose spelling is almost the same as X.

For example, "Kayla" has a high misspellability because there are many
names such as Karla, Layla, Kyla, Kaela, and Kaylia, which are less
popular than Kayla but which are spelled almost the same.

For this project, you will write two programs. Your first program,
`single`, will calculate the misspellabiilty of a single name in a
(large) list of first names.

The second program, `most`, will just read the (large) list of first
names, and find the first names which are most misspellable among them
all.

You may use any programming language as long as I can run it easily on
Linux (see details below).

## Honor

Take a moment to review the
[relevant section from the course
policy](https://usna.edu/Users/cs/roche/335/resources/policy.php#collaboration).

**If you have any doubt of what is allowed, just ask!**

## Similarity, popularity, and misspellability

We say two names are *similar* if the edit distance between them is
exactly one. Recall from class that this means you can turn one string
into the other string by adding one letter, removing one letter, or
switching one letter to a different letter.

For example, here are some pairs of similar names:

```
Mary Mark
Donald Ronald
Carol Carl
Jose Joe
Justin Austin
Teresa Theresa
Joan Juan
```

The *popularity* of a name is simply the number of times that name
appears in the list.

Finally, the *misspellability* of a name X is the sum, over all other
names Y and where Y is less popular than X, of the popularity of Y
divided by the popularity of X.

For this project, the misspellability will always be printed as a
percentage, rounded to the nearest whole percent.

For example, consider the following input list of n=30 names:

```
Dante
Lane
Dan
Dana
Dante
Jane
Lane
Ian
Dane
Dane
Don
Lane
Jane
Ian
Jane
Dan
Jane
Dante
Dante
Dane
Ian
Dana
Dana
Dane
Dan
Dane
Lane
Dana
Lana
Dane
```

To calculate the misspellability of "Dana", we first count how many
times Dana and all similar names to Dana appear:

*   Dana: 4 times
*   Dane: 6 times
*   Dan: 3 times
*   Lana: 1 time

Now we add up `(popularity of X) / (poularity of Dana)` for all X in the
list that are less popular than Dana. The only names similar to Dana and
less popular than it are "Dan" and "Lana", so this equals
`3/6 + 1/6`, which would be printed as a rounded
percentage as `67`.

If we look instead at `Dane`, it is similar to:

*   Dane: 6 times
*   Dante: 4 times
*   Lane: 4 times
*   Dana: 4 times
*   Jane: 4 times
*   Dan: 3 times

So the misspellability of Dane would be calculated as
`(4 + 4 + 4 + 4 + 3) / 6`, which is printed as a rounded percentage as
`317`.

## Warm-up: Calculate similarity

A **strongly suggested** first step exercise is to write a function in
your programming language like:

    bool is_similar(string name1, string name2);

which takes two names and returns true/false if they are similar
according to the definition above.

This is similar to the edit distance problem we looked at in class, but
is **much much simpler** because are only asking whether the edit
distance equals 1. In particular, you should not need to use any
complicated dynamic programming table to write this function
efficiently!

## Part 1: Misspellability of a particular name

Write a program called `single` that reads in a filename and a single
first name, then calculates the misspellabilituy of just that name among
the list of all names in the file.

Here is an example run. Your program would print out the prompts (up to
the colon), and the last line.

    File: med.txt
    Name: Dan
    840

Here, we typed `med.txt` and `Dan` from the command line, and the
program printed out 840, which is the misspellability of the name "Dan"
in that list of names.

One more example run:

    File: large.txt
    Name: Brian
    123

### Part 2: Most misspellable names

Copy your `single` program to a new program called `most`.

This program will read in a filename and a count of how many lines to
print. Then it will print out that many of the most misspellable names,
along with their misspellability scores, from most to least
misspellable.

Here are two example runs:

    File: med.txt
    Count: 10
    Aniya 992
    Lena 833
    Mara 800
    Hana 700
    Alina 693
    Alisa 673
    Kara 662
    Kali 647
    Talia 635
    Javon 632

Everything after the first two lines is the program's output, which in
this case contains the top 10 most misspellable names from `med.txt`.

    File: large.txt
    Count: 5
    Arin 1218
    Kasha 1159
    Jasha 1144
    Kela 1140
    Jana 1117

## Parameters

Your goal is to make your program as fast as possible, in terms of three
parameters:

*   *n* is the number of names in the given list.
    In all tests, it will never exceed **500 million**.
*   *k* is the number of *unique* names (not counting repeats). 
    In all tests, it will never exceed **100 thousand**.
*   *m* is the *maximum length* of each name (as a string).
    In all tests, it will never exceed **20**.

## What to turn in

Submit to [submit.moboard.com](https://submit.moboard.com/) under SI335
and assignment name `proj2`. Your submission should contain three files:

*   Your source code for Part 1, contained in a single file called
    `single.cpp` or similar (see table below under Languages)

*   Your source code for Part 2, contained in a single file called
    `most.cpp` or similar (see table below under Languages)

*   An `README.txt` file that:

    +   Has your name
    +   Cites (specifically!) any references you used in accordance with
        the collaboration policy
    +   Explains clearly how your program works
    +   Briefly explains how you came up with your brilliant idea
    *   Gives an analysis of the worst-case running time of your
        algorithm in terms of *n*, *k*, and *m* (see parameters above).

## Grading

Your grade will be calculated as follows.

*   Correctness: 60%

    Does your program always return the correct answer on all test
    cases, within at most 20 seconds runtime? (The test cases for
    correctness will not go up to the largest possible sizes.)

    +   Correctness of `single`: 30%
    +   Correctness of `most`: 30%

+   Efficiency: 30%

    Does your program run quickly on larger inputs (up to the parameters
    specified above)? To get the highest possible grade, your program
    should be able to handle the largest possible input in less than 10
    seconds runtime.

    +   Efficiency of `single`: 10%
    +   Efficiency of `most`: 20%

+   Analysis: 10%

    This is based on your `README` file having a clear, simple
    description of your your program works and an accurate worst-case
    runtime analysis.

## Example test files

A few files of names are included for your own testing. I will use
different (and sometimes larger) files for testing your code after
submission!

Most of the data comes from the [U.S. Social Security Administration's
lists of baby names](https://www.ssa.gov/oact/babynames/limits.html).

*   [`tiny.txt`](tiny.txt) n=30, k=9, m=5
*   [`small.txt`](small.txt) n=24326, k=3394, m=11
*   [`med.txt`](med.txt) n=112760, k=27518, m=15
*   [`large.txt`](large.txt) n=3778860, k=27518, m=15

## Languages

Your two programs must be called `single` and `most`, and can be written
in any programming language as long as I can run it.

Here are the "standard" languages:

Language | Source code filename
-------- | --------------------
C        | `single.c`
C++      | `single.cpp`
Java     | `Single.java` (and your `main` must be in the `Single` class)
Python3  | `single.py`
Rust     | `single.rs`
Haskell  | `single.hs`

Use a similar naming scheme for the `most` program.

To use one of these languages, just put *all* of your source code into a
file with the given name and submit it.  **You must use the names above
and put all your source code in a single file**.

(Note, for Java, it *is* possible to put multiple `class`es in the same
`.java` file as long as only the class with the `main` method is `public`.)

If you want to use a different language than the ones listed, send me an
email.

## Downloading this repo

To download ("clone") this repository, run from a linux command-line:

```bash
git clone https://github.com/si335usna/wrong-name.git
```

This will create a directory `wrong-name` from wherever you ran that
command, with all of these files. You can `cd` into that directory and
get to work!

Later, if some updates get made to this starter code repository and you
want to copy them to your local copy, you can just run:

```bash
git commit -am "saving my code"
git pull -s recursive -X ours origin main
```

I *strongly encourage* you to save your work using GitHub (or BitBucket
or GitLab or any other git-hosting service). For example, if you create
a free github account with username `myself`, then create a repository
(click the big + sign) called `myrepo`, you can connect that to your
local version by running

```bash
git remote add mine https://github.com/myself/myrepo
git push -u mine main
```

**Note**: Make sure your repository is *private*; otherwise you are
sharing your solutions with the world and probably violating the course
policy.
