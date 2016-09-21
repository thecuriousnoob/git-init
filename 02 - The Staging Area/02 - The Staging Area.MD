#Chapter II - The Staging Area

You've initialized a Git repository in your working folder and have done some stuffs you want to commit. It's great ! But before doing your commit, you first have to deal with the Staging Area.

This chapter will give you some tools about this.

##What is the Staging Area ?
Considering a commit as a snapshot of all the files you've edited you can think of the Staging Area as the photobooth in which you have to gather the files to get a snapshot of.

In this area you can add files you want to commit, remove some (definitely or not) or not.

##Tracked files and untracked files

At this point, if you run `git status` command you should obtain this response :

```
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	myAwesomeFile1.file
        myAwesomeFile2.file

nothing added to commit but untracked files present (use "git add" to track)
```

When a new file is added to a Git repository and has never been committed its changes are not tracked by Git. So are they considered as Untracked. In the other case, they would be tracked and we'll see later that this can lead up to some pretty cool shortcuts.

##git add

So for now we want to get our new files tracked by Git and we need to take a snapshot of these files first. So... let's add them to the Staging Area !

We will use `git add` command. There are various ways to use this command :

```
$ git add <file1> <file2> ... <fileN>
```

or in a more brutal way if you really want to add all your files without typing each file name you can just run :

```
$ git add --all
```

BUT be careful with this command as it adds ALL of the files. Be sure to control which file you get onto the Staging Area as you don't know yet how to undo a committing mistake ;-)

After adding your files, `git status` commands returns :

```
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   myAwesomeFile1.file
	new file:   myAwesomeFile2.file

```

Now your changes are set on the Staging Area and ready to be committed !

##git reset

If you're paying attention to what Git returns in the terminal you might have noticed this hint:

```
  (use "git reset HEAD <file>..." to unstage)
```

Well this says it all: this will allow you to unstage files from the Staging Area. This command will be useful in case you've misstaged some files.

As well as `git add` you can list numerous files before running the command and then if you'd like to unstage all staged files at once, here's the trick:

```
git reset HEAD *
``` 

##git checkout -- <file>

Consider now that you've made some changes you want to discard from your working tree. Here's the command that you'll need to run. This will discard changes in the specified files *that are not added to your indexed changes yet* (modified files where you didn't already run `git add` on).

```
git checkout -- <file>
```

Note that you can use the * trick as well if you wish to discard all changes from your working tree.

Also note that if you want to discard changes from an indexed file you'll first need to run `git reset HEAD <file>` so it drops the file from your index to your working tree and then you'll be able to `git checkout --` that file.

##git rm

If you want to completely get rid of a file (from your index and your working tree as well) then you can run:

```
git rm <file1> <file2> ... <fileN>
```

Use this one with extreme care since you won't be able to get back your files then !

---

Go to the [previous chapter](../01 - git init/01 - git init.MD) or to the [next chapter](../03 - Commits/03 - Commits.MD) or [back to the home page](../README.MD). 
