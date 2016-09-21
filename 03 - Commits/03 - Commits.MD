#Chapter III - Commits

All modified files have been staged and here you are ready to take a snapshot of your project. Time has come for you to commit your changes !

This chapter is going to show some commands to deal with commits. Get ready to be a commit king !

##git commit

A commit is a snapshot of some modifications brought to some files referenced by a hash and a message.

To commit your staged changes run:

```
$ git commit
```

You should get invited to type in a commit message: be short and explicit about what you did !

Once you're done with the message, you'll see some computing and then a summary of your committed changes :

```
[master 1f7f655] Add text in myAwesomeFile1
 1 files changed, 1 insertion(+)
```

You'll see some informations about your commit :

* `master` is the branch on which you just committed,
* `1f7f655` is a unique hash identifying your commit.

Both of these informations are right next to your commit message. Then we have:
* the total number of files changed,
* the total number of insertions (number of lines you've added) and/or deletions (number of lines you've deleted).

###`-a`

Once a file gets committed it gets tracked by Git. In this case if we modify that file later and would like to commit these changes we could use a short cut to skip on the `git add` step by running `git commit -a`.

Like mentionned: this shortcut will work only on tracked files. Any untracked file won't be added. You have to add them manually using `add` command.

Example:

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   myAwesomeFile1

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	myAwesomeFile3

no changes added to commit (use "git add" and/or "git commit -a")

$ git commit -a
[master cf4b38f] Update text in myAwesomeFile1
 1 file changed, 1 insertion(+)

```

We can already see that only one file has been changed in our newly created commit. Running `git status` again right after this commit we would get:

```
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	myAwesomeFile3

nothing added to commit but untracked files present (use "git add" to track)
```

###`-m`

Another cool shortcut is this one. When you frequently use Git you can get tired with all the gitCommitOpenEditorTypeYourMessageSaveQuit process, so Git provides this `-m` option to `git commit` so you can directly type in a short commit message !

Just pay an extreme care to the quotes ! Don't forget to surround your message with it ;-)

```
$ git commit -m "Update in myAwesomeFile2"
[master 2c6dccc] Update in myAwesomeFile2
 1 file changed, 1 insertion(+)
```

How cool is that ? :-) Well, we have more to see !

###`--amend`

You've just committed some changes. Cool ! But you've just forgot to add a bunch of modifications in this commit. Crap ! What can we do ? Aw and my commit message will no longer be explicit if I add these modifications...

Stop ! Keep calm and use `git commit --amend` ;-) This will solve both of the problems mentionned above and here's how :

* Add your files to the staging area using either `git add` or `-a` option if your files are already tracked
* Then run `git commit --amend` (which of course you can combine with `-a` and `-m` options)
* If you haven't used `-m` option an editor will open up so you can edit your previous commit message.

```
$ git show HEAD
[master 70d9dce] Awesome change in myAwesomeFile3
 Date: Tue Sep 20 17:24:16 2016 +0200
 1 files changed, 3 insertions(+)
 create mode 100644 myAwesomeFile3

$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   myAwesomeFile1

no changes added to commit (use "git add" and/or "git commit -a")

$ git commit --amend -am "Awesome change in myAwesomeFile3 and myAwesomeFile1"
[master 62ea6fc] Awesome change in myAwesomeFile3 and myAwesomeFile1
 Date: Tue Sep 20 17:24:16 2016 +0200
 2 files changed, 4 insertions(+)
 create mode 100644 myAwesomeFile3
```

In this example we first display our last commit using `git show HEAD`. Its informations are :
* Hash : `70d9dce`,
* Message : `Awesome change in myAwesomeFile3 and myAwesomeFile1`,
* Files changed : 1 (myAwesomeFile3).

Then we do some changes in `myAwesomeFile1` and run a `git status` to check if the file is tracked (and it is !).

So we can now run our super combo command `git commit --amend -am "yeah"` which says "amend the last commit with the files in the Staging Area and rewrite the message to 'yeah'".

As a response we'll get some updated informations about our commit :
* Hash : `62ea6fc` which is new,
* Message : `Awesome change in myAwesomeFile3 and myAwesomeFile1`,
* Files changed : 2 (myAwesomeFile3 and myAwesomeFile1 though it's not printed out).

##git log

A cool command to check you commits history in git is `git log`.

```
$ git log
commit 62ea6fcd3cb9c48a41a4da23e33dcd01f55cc489
Author: thecuriousnoob <thecuriousnoob@johndoe.com>
Date:   Tue Sep 20 17:24:16 2016 +0200

    Awesome change in myAwesomeFile3 and myAwesomeFile1

commit cf4b38f44ee1eea922c0d03fad1bae75d317a6f7
Author: thecuriousnoob <thecuriousnoob@johndoe.com>
Date:   Tue Sep 20 17:17:00 2016 +0200

    Awesome change in myAwesomeFile2
```

###`--oneline`
This option will list your commits history but will display each commit on one line. So if your commit message is more than one line long only the very first line will be displayed.

I really like this option as it allows you to have a quick glance at the essential informations of your last commits.

```
$ git log --oneline
62ea6fc Awesome change in myAwesomeFile3 and myAwesomeFile1
cf4b38f Awesome change in myAwesomeFile2
```

##git reset: the return

Remember `git reset` ? We've used this command in the previous chapter to unstage files. Well guess what ? This command has some more to offer !

###`--soft`

You've committed changes but you want to do some more changes on your files. We've seen that we could amend our last commit. But if we also want to undo/edit some older changes in older commits amend option won't be useful. Well `git reset --soft` will do the trick, and here's how.

By typing `git reset --soft HEAD~<numberofcommitstoreset>` we will drop our commits and keep our changes in the Staging Area, ready to be committed. See example below :

```
$ git log --oneline
cf4b38f Awesome change in myAwesomeFile2
36cf4b5 Creation of myAwesomeFile2 and myAwesomeFile3
48ef512 Creation of myAwesomeFile1

$ git reset --soft HEAD~2

$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   myAwesomeFile1
	new file:   myAwesomeFile2
	new file:   myAwesomeFile3

$ git log --oneline
48ef512 Creation of myAwesomeFile1
```

###`--hard`

This is an option you would use if you're really angry at someone for his work. `git reset --hard` is used just like `git reset --soft` except that *IT DROPS ALL OF YOUR CHANGES*. So it must be used with *EXTREME CARE* knowing exactly what you're doing.

Example :

```
$ git log --oneline
cf4b38f Awesome change in myAwesomeFile2
36cf4b5 Creation of myAwesomeFile2 and myAwesomeFile3
48ef512 Creation of myAwesomeFile1

$ git reset --hard HEAD~2
HEAD is now at 48ef512 Creation of myAwesomeFile1

$ git status
On branch master
nothing to commit, working directory clean

$ git log --oneline
48ef512 Creation of myAwesomeFile1
```

---

Go to the [previous chapter](../02 - The Staging Area/02 - The Staging Area.MD) or [back to the home page](../README.MD).
