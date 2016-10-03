#Chapter I - git init

First we'll see `git init` command and a bit of what happens under the layer.

##Summary
 * [git init](#git-init)
 * [git status](#git-status)
 * [Further explanations](#further-explanations)

##git init
This command initializes a new empty git repository in your working folder.

You can type this command into any folder you'd like to manage with git even though it already contains files or not.
To do so, simply type in your command:

```
$ git init
```

You should get this as a result :

```
Initialized empty Git repository in /path/where/you/work/
```

However if you already initialized your repository or cloned an existing repository you don't need to use `git init`.
If you do you'll get this as a result :

```
Reinitialized existing Git repository in /path/where/you/work
```

Once you've initialized your Git repository you're ready to go !

##git status
A really healthy command to run is `git status`. This will give you the state of your Git repository.

It's really good to often run `git status`. At some point it becomes a reflex.

Here's what `git status` would return if you run it in your newly initialized repository :

```
On branch master

Initial commit

nothing to commit (create/copy files and use "git add" to track)
```

So remember to run as often as you can `git status` ! This can save your life, trust me ;-)

##Further explanations
What happens when you execute `git init` command ?

Well if you type in `ls -a` you should see a new hidden folder named `.git`.

`git init` command creates that new folder. Now simply execute `ls -F1 .git/` to list its contents :

```
HEAD
branches/
config
description
hooks/
info/
objects/
refs/
```

`.git` folder contains everything essential to Git to manage your files correctly.

* `HEAD` points to the actual branch you've checked out (see 04 - Git Branch for more informations about branches and checkout),
* `branches/` has no particular purpose today but stands as a store for shorcuts URL to branches you pull and push (see [this link](http://stackoverflow.com/questions/10398225/what-is-the-git-branches-folder-used-for) for detailed informations),
* `config` contains any project-specific configuration options,
* `description` is used by the GitWeb program to display the description of the repository on GitWeb page,
* `hooks/` contains hooks scripts (see [Git documentation on hooks](https://git-scm.com/book/en/v2/ch00/_git_hooks) for more informations about hooks)
* `info/` keeps a file to exclude patterns you don’t want to track in a .gitignore file (see 02 - Git Add for more informations about .gitignore)
* `objects/` stores all the content in your database,
* `refs/` stores pointers to commits in the data stored.

All of these files and folders are hidden in the `.git` repository. Though they exists as core components of Git, you won't need to access them. It's nice to know they're there though !

---

Go to the [next chapter](./02 - The Staging Area.MD) or [back to the home page](./README.MD).
