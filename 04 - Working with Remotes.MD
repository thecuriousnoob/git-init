#Chapter IV - Working with Remotes

The first big step to use git is to know how to commit some changes. Once done these changes are locally committed. This obviously means that if anything bad happens to your storage system, your work could get in trouble. Plus if you would like to share your work with peers it would get a bit tedious.

##Summary
 * [About remotes](#about-remotes)
 * [Add a remote](#add-a-remote)
 * [List remotes](#list-remotes)
 * [Renaming a remote](#renaming-a-remote)
 * [Deleting a remote](#deleting-a-remote)
 * [Pushing your changes to a remote](#pushing-your-changes-to-a-remote)

##About remotes
Let's talk about remotes which are remote hosts for your work somewhere on the Internet (like this repository on GitHub is a remote host of my local repository for git-init).

As a prerequisite you need to get a URL to locate your remote repository which can be either an HTTPS URL or a SSH URL.

A repository can have multiple remotes so you have the possibility to identify your remotes with a name. For example, your default remote will be named `origin`.

##Add a remote
To add a remote you must tell git to add a remote called `<yourremotename>` and located at `<yourremoteurl>`.

So we simply need to run :

```
$ git remote add origin https://github.com/thecuriousnoob/git-init.git
```

##List remotes
We've just added a remote to our repository but you might have noticed that the console doesn't return you any information about it. So if you want to make sure that your operation was successful you can list your configured remotes by simply running :

```
$ git remote
origin
```

Then if you want more informations such a remotes URLs you can use `-v` option :

```
$ git remote -v
origin	https://github.com/thecuriousnoob/git-init.git (fetch)
origin	https://github.com/thecuriousnoob/git-init.git (push)
```

`fetch` and `push` means that you can pull/push contributions from/to these repositories.

##Renaming a remote
We're happy, suppose we've added a remote named `remote` but obviously this is a terrible name. So we want to change that name to something more explicit such as `production`.

Guess what ? There's a command to do that !

```
$ git remote rename <oldname> <newname>
```

So to complete our example just see the following :

```
$ git remote
origin
remote

$ git remote rename remote production

$ git remote
origin
production
```

##Deleting a remote
Finally, we've observed that our `production` remote is no longer used. To avoid polluting your repository with useless remotes you can delete them with one command :

 ```
 git remote rm <remotename>
 ```

As an example :

```
$ git remote
origin
production

$ git remote rm production

$ git remote
origin
```

##Pushing your changes to a remote
Once you are ok with your commits and remote configuration the only thing left is to push your commits to the remote using `git push` command !

The basic syntax for this command is `git push <remotename> <branchname>` which means "Git, push my commits on the branche <branchname> of remote <remotename>".

Once you run this command you'll see the push operation running. And that's it !

```
$ git push origin master

Counting objects: 7, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (7/7), 1.84 KiB | 0 bytes/s, done.
Total 7 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/thecuriousnoob/git-init.git
   b60ffb0..d87bead  master -> master
```

###`-f` option, be careful when using the Force
In case you've already pushed a commit to your remote and decided to amend this commit locally, if you try pushing this commit you'll get an error ! In fact your original commit is identified by some hash on the remote (e.g. `63efb56`) and as you've seen in the [previous chapter](./03 - Commits.MD), when you amend a commit, its hash changes !

This means the remote HEAD is not pointing at the same reference than the local HEAD.

```
REMOTE
+---------+    +---------+    +---------+
+ 3e3fb65 +--->+ 3eafb35 +--->+ 63efb56 |
+---------+    +---------+    +---------+
                                   |
                                  HEAD
LOCAL
+---------+    +---------+    +---------+
+ 3e3fb65 +--->+ 3eafb35 +--->+ a6345fe |
+---------+    +---------+    +---------+
                                   |
                                  HEAD
```

The remote expects you to push this :

```
+---------+    +---------+    +---------+    +---------+
+ 3e3fb65 +--->+ 3eafb35 +--->+ 63efb56 |--->+ a6345fe |
+---------+    +---------+    +---------+    +---------+
                                                  |
                                                 HEAD
```

But since it can't find commit `63efb56`, he will throw you an error saying that some refs are missing. But since `63efb56` doesn't exist anymore locally we need to replace it by `a6345fe` on the remote.

Boohoohoo example :

```
$ git push origin master

To https://github.com/thecuriousnoob/git-init.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/thecuriousnoob/git-init.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```


To fix that, we must use something only wise Jedis can use.

*Something that you have to use with an extreme care and only in some precise cases.*

Use `-f` option a.k.a The Force.

```
$ git push -f origin master

Counting objects: 7, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (7/7), 2.66 KiB | 0 bytes/s, done.
Total 7 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/thecuriousnoob/git-init.git
 + d87bead...4aab063 master -> master (forced update)

```

*/!\ Reminder : Use this with an extreme care and only in some precise cases.*

---

Go to the [previous chapter](./03 - Commits.MD) or [back to the home page](./README.MD).
