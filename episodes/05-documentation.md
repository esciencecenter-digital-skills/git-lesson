---
title: Document your research software
teaching: 25
exercises: 0
---

::::::::::::::::::::::::::::::::::::::: objectives

- Understand the importance of writing code documentation together with the source code
- Know what makes a good documentation
- Learn what tools can be used for writing documentation
- Be able to motivate a balanced decision: sometimes READMEs are absolutely enough

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions


- What tools are out there?
- What are their pros and cons?


::::::::::::::::::::::::::::::::::::::::::::::::::

## Why we teach this lesson

Everyone should document their code, even if they're working alone.

These are the main points:
- Code documentation has to be versionnable and branchable
- Code documentation should be tracked together with the source code
- README is often enough

**Please do not skim over the two above points**. Please take few minutes to
explain why documentation (sources) should be tracked together with the source
code.  Please discuss this aspect with workshop participants and connect it to
**reproducibility**. This is for me (Radovan) the most important take-home
message.

Specific motivations:

- Code documentation becomes quickly unmanageable if not part of the source code.
- It helps people to quickly use your code thus reducing the time spent to explain over and again to new users.
- It helps people to collaborate.
- It improves the design of your code.

:::::::::::::::::::::::::::::::::::::::::  callout

## In-code documentation

Above we used

Comments, function docstrings
- Advantages
- Good for programmers
- Version controlled alongside code
- Can be used to auto-generate documentation for functions/classes
- Disadvantage
- Probably not enough for users of the code


::::::::::::::::::::::::::::::::::::::::::::::::::

Other topic

:::::::::::::::::::::::::::::::::::::::::  callout

## README files

If you read the output of `git status` carefully,
you'll see that it includes this hint:

```output
(use "git checkout -- <file>..." to discard changes in working directory)
```

As it says,
`git checkout` without a version identifier restores files to the state saved in `HEAD`.
The double dash `--` is needed to separate the names of the files being recovered
from the command itself:
without it,
Git would try to use the name of the file as the commit identifier.


::::::::::::::::::::::::::::::::::::::::::::::::::

The fact that files can be reverted one by one
tends to change the way people organize their work.
If everything is in one large document,
it's hard (but not impossible) to undo changes to the introduction
without also undoing changes made later to the conclusion.
If the introduction and conclusion are stored in separate files,
on the other hand,
moving backward and forward in time becomes much easier.

:::::::::::::::::::::::::::::::::::::::  challenge

## Recovering Older Versions of a File

Jennifer has made changes to the Python script that she has been working on for weeks, and the
modifications she made this morning "broke" the script and it no longer runs. She has spent
\~ 1hr trying to fix it, with no luck...

Luckily, she has been keeping track of her project's versions using Git! Which commands below will
let her recover the last committed version of her Python script called
`data_cruncher.py`?

1. `$ git checkout HEAD`

2. `$ git checkout HEAD data_cruncher.py`

3. `$ git checkout HEAD~1 data_cruncher.py`

4. `$ git checkout <unique ID of last commit> data_cruncher.py`

5. Both 2 and 4

:::::::::::::::  solution

## Solution

The answer is (5)-Both 2 and 4.

The `checkout` command restores files from the repository, overwriting the files in your working
directory. Answers 2 and 4 both restore the *latest* version *in the repository* of the file
`data_cruncher.py`. Answer 2 uses `HEAD` to indicate the *latest*, whereas answer 4 uses the
unique ID of the last commit, which is what `HEAD` means.

Answer 3 gets the version of `data_cruncher.py` from the commit *before* `HEAD`, which is NOT
what we wanted.

Answer 1 can be dangerous! Without a filename, `git checkout` will restore **all files**
in the current directory (and all directories below it) to their state at the commit specified.
This command will restore `data_cruncher.py` to the latest commit version, but it will also
restore *any other files that are changed* to that version, erasing any changes you may
have made to those files!
As discussed above, you are left in a *detached* `HEAD` state, and you don't want to be there.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Reverting a Commit

Jennifer is collaborating with colleagues on her Python script.  She
realizes her last commit to the project's repository contained an error, and
wants to undo it.  Jennifer wants to undo correctly so everyone in the project's
repository gets the correct change. The command `git revert [erroneous commit ID]` will create a
new commit that reverses the erroneous commit.

The command `git revert` is
different from `git checkout [commit ID]` because `git checkout` returns the
files not yet committed within the local repository to a previous state, whereas `git revert`
reverses changes committed to the local and project repositories.

Below are the right steps and explanations for Jennifer to use `git revert`,
what is the missing command?

1. `________ # Look at the git history of the project to find the commit ID`

2. Copy the ID (the first few characters of the ID, e.g. 0b1d055).

3. `git revert [commit ID]`

4. Type in the new commit message.

5. Save and close

:::::::::::::::  solution

## Solution

The command `git log` lists project history with commit IDs.

The command `git show HEAD` shows changes made at the latest commit, and lists
the commit ID; however, Jennifer should double-check it is the correct commit, and no one
else has committed changes to the repository.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Understanding Workflow and History

What is the output of the last command in

```bash
$ cd planets
$ echo "Venus is beautiful and full of love" > venus.txt
$ git add venus.txt
$ echo "Venus is too hot to be suitable as a base" >> venus.txt
$ git commit -m "Comment on Venus as an unsuitable base"
$ git checkout HEAD venus.txt
$ cat venus.txt #this will print the contents of venus.txt to the screen
```

1. ```output
  Venus is too hot to be suitable as a base
  ```
2. ```output
  Venus is beautiful and full of love
  ```
3. ```output
  Venus is beautiful and full of love
  Venus is too hot to be suitable as a base
  ```
4. ```output
  Error because you have changed venus.txt without committing the changes
  ```

:::::::::::::::  solution

## Solution

The answer is 2.

The command `git add venus.txt` places the current version of `venus.txt` into the staging area.
The changes to the file from the second `echo` command are only applied to the working copy,
not the version in the staging area.

So, when `git commit -m "Comment on Venus as an unsuitable base"` is executed,
the version of `venus.txt` committed to the repository is the one from the staging area and
has only one line.

At this time, the working copy still has the second line (and
`git status` will show that the file is modified). However, `git checkout HEAD venus.txt`
replaces the working copy with the most recently committed version of `venus.txt`.

So, `cat venus.txt` will output

```output
Venus is beautiful and full of love.
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Checking Understanding of `git diff`

Consider this command: `git diff HEAD~9 mars.txt`. What do you predict this command
will do if you execute it? What happens when you do execute it? Why?

Try another command, `git diff [ID] mars.txt`, where [ID] is replaced with
the unique identifier for your most recent commit. What do you think will happen,
and what does happen?


::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Getting Rid of Staged Changes

`git checkout` can be used to restore a previous commit when unstaged changes have
been made, but will it also work for changes that have been staged but not committed?
Make a change to `mars.txt`, add that change using `git add`,
then use `git checkout` to see if you can remove your change.

:::::::::::::::  solution

## Solution

After adding a change, `git checkout` can not be used directly.
Let's look at the output of `git status`:

```output
On branch main
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   mars.txt

```

Note that if you don't have the same output
you may either have forgotten to change the file,
or you have added it *and* committed it.

Using the command `git checkout -- mars.txt` now does not give an error,
but it does not restore the file either.
Git helpfully tells us that we need to use `git reset` first
to unstage the file:

```bash
$ git reset HEAD mars.txt
```

```output
Unstaged changes after reset:
M	mars.txt
```

Now, `git status` gives us:

```bash
$ git status
```

```output
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   mars.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

This means we can now use `git checkout` to restore the file
to the previous commit:

```bash
$ git checkout -- mars.txt
$ git status
```

```output
On branch main
nothing to commit, working tree clean
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Explore and Summarize Histories

Exploring history is an important part of Git, and often it is a challenge to find
the right commit ID, especially if the commit is from several months ago.

Imagine the `planets` project has more than 50 files.
You would like to find a commit that modifies some specific text in `mars.txt`.
When you type `git log`, a very long list appeared.
How can you narrow down the search?

Recall that the `git diff` command allows us to explore one specific file,
e.g., `git diff mars.txt`. We can apply a similar idea here.

```bash
$ git log mars.txt
```

Unfortunately some of these commit messages are very ambiguous, e.g., `update files`.
How can you search through these files?

Both `git diff` and `git log` are very useful and they summarize a different part of the history
for you.
Is it possible to combine both? Let's try the following:

```bash
$ git log --patch mars.txt
```

You should get a long list of output, and you should be able to see both commit messages and
the difference between each commit.

Question: What does the following command do?

```bash
$ git log --patch HEAD~9 *.txt
```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- `git diff` displays differences between commits.
- `git checkout` recovers old versions of files.

::::::::::::::::::::::::::::::::::::::::::::::::::


