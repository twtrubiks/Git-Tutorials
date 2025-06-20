[中文版](README.md)

# Git-Tutorials Basic Usage Guide :memo:

I found this stuff quite interesting, so I wrote a simple tutorial to document it :memo:, hoping to help those who want to learn :smile:

If there are any mistakes in the tutorial, please feel free to correct me :sweat_smile:

For basic commands and installation, you can refer to a video I made earlier:

* [Youtube Tutorial - Basic GitHub Tutorial - From Scratch](https://www.youtube.com/watch?v=py3n6gF5Y00)

The video tutorial includes how to generate an **SSH key**.

If the steps are correct and there are no errors, you should find a **.ssh folder** in the path, containing two files: **id_rsa** and **id_rsa.pub**.

These two are the SSH Key. **id_rsa is the private key** and should not be disclosed. **id_rsa.pub is the public key**, which you can safely share with anyone.

After installing Git, the first thing to do is to set your name and email:

```cmd
git config --global user.name "twtrubiks"
git config --global user.email "twtrubiks@gmail.com"
```

You can enter the following to confirm if the input was successful:

```cmd
git config --global user.name
git config --global user.email
```

![alt tag](https://i.imgur.com/5mpS7Ij.jpg)

To view Git configuration data, you can execute the following command (a more detailed tutorial will be at the end of the article):

```cmd
git config --list
```

## git init command

Initialize git

```cmd
git init
```

You can also specify a folder

```cmd
git init <directory>
```

## git clone command

Copy the URL from the location shown in the picture (don't copy mine~ copy your own)

![alt tag](https://i.imgur.com/EJ5JNjt.jpg)

git clone (copied URL) SSH / HTTPS

(If you want to use the https method, please see [Personal Access Tokens](https://github.com/twtrubiks/Git-Tutorials#personal-access-tokens))

```cmd
git clone git@github.com:twtrubiks/test.git
```

The first time, an SSH warning will appear, just select YES.

As shown in the picture (download successful), a new folder will appear in your download path.

![alt tag](https://i.imgur.com/iIkTlqf.jpg)

## Personal Access Tokens

* [Youtube Tutorial - GitHub Tutorial - Personal Access Tokens](https://youtu.be/aJRRVCB85k8)

Starting from August 13, 2021, if you use the https method, you will find:

![alt tag](https://i.imgur.com/6YIJSaj.png)

```text
remote: Support for password authentication was removed on August 13, 2021.
remote: Please see https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls for information on currently recommended modes of authentication.
fatal: Authentication failed for 'https://github.com/xxxxx.git/'
```

At this point, if we don't want to add an ssh key, nor add collaborators, we can use Personal Access Tokens (you can think of it as a temporary permission).

First, go to your GitHub's Settings -> Developer settings,

Select Personal Access Tokens, and generate your token.

![alt tag](https://i.imgur.com/zPVlOjf.png)

You can define how long the token will be valid.

The section below defines the permissions for this token.

![alt tag](https://i.imgur.com/NNJcYRM.png)

After setting it up, you can copy your token.

![alt tag](https://i.imgur.com/qhtIBn.png)

Then go back and use the https clone method.

Originally, you used username + password (no longer usable).

Now, change it to username + the token you just got, and you can clone successfully.

### How to improve (speed up) git clone for large repos

* [Youtube Tutorial - How to improve (speed up) git clone for large repos](https://youtu.be/YHX0qkQa1UI)

Sometimes we need to clone very large repos, and `git clone` takes a long time. Is there a way to speed up the cloning process? :question:

Let's try it out (using [django](https://github.com/django/django) as an example).

`git clone git@github.com:django/django.git`

(You will find that cloning takes some time :triumph:)

![alt tag](https://i.imgur.com/yMH6L8F.png)

Next, check the log, `git log`

![alt tag](https://i.imgur.com/vJkFTr2.png)

Try switching branches `git checkout stable/2.2.x`

![alt tag](https://i.imgur.com/UtxJ2ER.png)

Let's start improving (speeding up) the clone time.

You can do this with the `--depth` parameter. Simply put, when we normally clone and then run `git log`, you will see a large number of logs. In some cases, you may not need so many logs.

That is, you may only need the last 10 history commits, or even just 1 (meaning you don't need history commits at all). This is where `--depth` is very suitable.

`git clone git@github.com:django/django.git --depth 1`

(You will find it's much faster this time)

![alt tag](https://i.imgur.com/yvkZUZI.png)

Next, check the log, `git log`
(The reason it's faster is that we only keep the latest history commit. If you need the last 10, change it to --depth 10)

![alt tag](https://i.imgur.com/at9Zzq3.png)

But there will be a problem when you try to switch branches `git checkout stable/2.2.x`

(You will find that you cannot switch to a remote branch :scream:

The reason is that using `--depth` is equivalent to `--single-branch`, so of course, there are no other branches.)

![alt tag](https://i.imgur.com/gDaeq1W.png)

That is to say, the following two commands are actually equivalent:

```cmd
git clone git@github.com:django/django.git --depth 1
git clone git@github.com:django/django.git --depth 1 --single-branch
```

To solve this problem, a better way is:

```cmd
git clone git@github.com:django/django.git --depth 1 --no-single-branch
```

(This will be slightly slower than `--single-branch` because the latest history commit of each branch needs to be cloned.)

This way, you can keep the remote branches.

![alt tag](https://i.imgur.com/BkLKVZz.png)

Successfully switched to the remote branch, `git checkout stable/2.2.x`.

![alt tag](https://i.imgur.com/VCvcSTr.png)

Finally, a quick summary:

To clone the latest history and also need other branches, use the following:

`git clone git@github.com:django/django.git --depth 1 --no-single-branch`

If you want to specify a branch, add `-b`:

`git clone git@github.com:django/django.git --depth 1 --no-single-branch -b stable/3.1.x`

To clone the latest history and **do not** need other branches, use the following:

`git clone git@github.com:django/django.git --depth 1 --single-branch`

or

`git clone git@github.com:django/django.git --depth 1`

For more detailed parameter descriptions, please refer to [git clone](https://git-scm.com/docs/git-clone)

## git status command

```cmd
git status
```

Allows us to view the current repository (repo container).

![alt tag](https://i.imgur.com/5Gt98Vh.jpg)

This means your working directory is currently clean.

## Working Directory and Staging Area (Stage)

`git add` means to put the files to be committed into the staging area (Stage).

Then execute

`git commit` to send all modified content in the staging area (Stage) to the current branch.

Once committed (`git commit`), if you haven't made any changes to the working directory, then the working directory is "clean".

`git commit -m "xxxxx"` command, the content after -m is the description of this modification (commit).

Try to enter content that makes it clear at a glance what was modified in this commit (for easy future reference to quickly understand what was changed in this commit).

The following demo shows adding a Hello.py file to a folder.

Then use `git status` to view the current repository (repo container), you will see that Hello.py is untracked, as shown below:

![alt tag](https://i.imgur.com/dvj1DQh.jpg)

You can use the following command:

```cmd
git add Hello.py
```

Extra tip, this command is very interesting, everyone can play with it:

```cmd
git add -p
```

Then use

`git commit -m "text"`

```cmd
git commit -m "add Hello.py"
```

Use `git status` again, and you will find that the working directory is clean. As shown below:

![alt tag](https://i.imgur.com/6VrieNb.jpg)

Additionally, if you only enter

```cmd
git commit
```

![alt tag](https://i.imgur.com/yZxKGTU.jpg)

An editor window will pop up.

![alt tag](https://i.imgur.com/htNQ0dJ.jpg)

At this point, you can press the **Ins key** (or the **letter i** on the keyboard) to enter text.

![alt tag](https://i.imgur.com/NFy16dp.jpg)

After entering the text, first press the **Esc key**. After pressing it, the INSERT at the bottom will disappear. Then type **:wq** and press enter to save and exit.

For more parameters, please refer to the [https://git-scm.com/docs/git-commit](https://git-scm.com/docs/git-commit) documentation.

**How to modify the last commit?**

Sometimes after we commit, we realize we made a typo in the commit message.

At this time, you can use the following command, which will pop up an editor window for you to edit your last commit message.

```cmd
git commit --amend
```

Or, after we commit, we realize we missed adding a few files.

At this time, you can use the following command:

```cmd
git commit -m "init commit"
git add missing_file.py
git commit --amend
```

The above situation is when after `git commit -m "init commit"`,

I found that I missed the **missing_file.py** file (forgot to add it before committing).

At this time, you can use `git commit --amend` to modify the last commit.

Sometimes, for convenience, we directly use the following command to add all files at once:

```cmd
git add .
```

But after adding, we find that some files did not need to be added. At this time, you can use the following command to un-add them:

```cmd
git reset HEAD <file>
```

Example: There are two files, A.py and B.py, in the path, and I use **git add .** to add them.

![alt tag](https://i.imgur.com/0S7TcEB.jpg)

But after adding, I realize that I don't want to add B.py yet, so I can use **git reset HEAD B.py** to revert it.

![alt tag](https://i.imgur.com/3iAyEEx.jpg)

## git push command

```cmd
git push
```

Push the code to GitHub (or Bitbucket, etc.), as shown below:

![alt tag](https://i.imgur.com/d61Pau6.jpg)

## Version Control - History

```cmd
git log
```

Press **lowercase q** to exit.

![alt tag](https://i.imgur.com/j11afCP.jpg)

If you find the layout too cluttered, you can use the following command:

```cmd
git log --pretty=oneline
```

Press **lowercase q** to exit.

![alt tag](https://i.imgur.com/jz2cwUA.jpg)

If you want to see the changes of a specific file or folder, you can use it like this, for example:

* [Youtube Tutorial - Git Log: Log disappears after moving a folder? Use --follow to find file history! (To be added)](xx)

```cmd
git log -- folder
```

If tracking individual files, you can add `--follow`

```cmd
git log --follow -- folder/demo.py
```

For example, I have a folder structure as follows:

```cmd
❯ tree
.
├── production
│   ├── a
│   │   ├── a1.txt
│   │   ├── a2.txt
│   │   └── a3.txt
│   └── b
│       └── b1.txt
└── test
```

History log under `production`:

```cmd
❯ git log -- production/a

* b9a481b - a3.txt
* 02fce19 - a2.txt
* 1e4aa1b - create
```

Suppose today we move the `a` folder under `production` to the `test` folder,

The folder structure becomes as follows, then commit:

```cmd
❯ tree
.
├── production
│   └── b
│       └── b1.txt
└── test
    └── a
        ├── a1.txt
        ├── a2.txt
        └── a3.txt
```

The current git log of the entire repo is as follows:

```cmd
❯ git log

* 5707ce2 - move
* b9a481b - a3.txt
* 02fce19 - a2.txt
* 1e4aa1b - create
* 1b7fb87 - Initial commit
```

Then look at the `a` folder, as follows:

```cmd
❯ git log -- test/a

* 5707ce2 - move
```

You will find that the git tracking records for `a2.txt` and `a3.txt` have disappeared!!!

Method 1, track the original folder.

Although this file no longer exists, the record is still in git.

```cmd
# Here you will find that the folder no longer exists because it has been moved
❯ ls production/a

ls: cannot access 'production/a': No such file or directory

# But you can still track the history
❯ git log -- production/a

* 5707ce2 - move
* b9a481b - a3.txt
* 02fce19 - a2.txt
* 1e4aa1b - create
```

Method 2, add `--follow`. This can track individual files (don't use it for moved folders, as you won't see past records).

```cmd
❯ git log --follow -- test/a/a1.txt

* 5707ce2 - move
* 1e4aa1b - create
```

Also, here is another way to view the log (very cool :satisfied:), feels like a GUI (source is from the link at the end of the article).

```cmd
git log --graph --pretty=format:"%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset" --abbrev-commit --date=relative
```

![alt tag](https://i.imgur.com/XNQisuf.png)

In Git, HEAD is used to represent the current version.

```cmd
git reset --hard HEAD
```

![alt tag](https://i.imgur.com/pkFO8pk.jpg)

If you now want to revert the current version to the previous version, you can use the `git reset` command:

The previous version is HEAD~1.

```cmd
git reset --hard HEAD~1
```

![alt tag](https://i.imgur.com/ZThoaUT.jpg)

The version before that is HEAD~2.

To revert to a specific version:

![alt tag](https://i.imgur.com/KrCOC71.jpg)

```cmd
git reset --hard ad41df36b7
```

The `--hard` parameter has three options: `--mixed` (default), `--hard`, `--soft`.

`--hard` simply means to discard all previous commits (completely **not preserved**).

`--soft` simply means to discard all previous commits, but **preserve** the state of your previous working directory.

I think `--hard` and `--soft` are not easy to explain with words. I suggest everyone try them out to understand the difference.

`--soft` is very suitable for merging multiple meaningless commits into one commit.

![alt tag](https://i.imgur.com/6RVutiK.jpg)

The version number (ad41df36b7) doesn't need to be written in full, just the first few digits are enough, Git will find it automatically.

When you revert to a certain version and suddenly regret it the next day, how do you restore to the previous new version?

What if you can't find the commit id of the new version?

At this time, you can use a command:

```cmd
git reflog
```

![alt tag](https://i.imgur.com/MaRlZZr.jpg)

Then see which version you want to go back to, and use `git reset`.

```cmd
git reset --hard 642e7af
```

Sometimes you want to eliminate (overwrite) a commit that has already been pushed. At this time, we can use:

```cmd
git push --force
```

Or a shorter way:

```cmd
git push -f
```

You can force push. First, go back to a certain version, and then force push.

***Note! When working on a multi-person project, try not to use methods like --force, because sometimes it will harm others. It is recommended to use revert.***

For the above reason, it is recommended to use a safer way:

```cmd
git push --force-with-lease
```

This can ensure that you don't accidentally discard someone else's commit. (If someone commits and pushes before you, you will not be able to push to the remote).

## checkout

Please also refer to [git switch](https://github.com/twtrubiks/Git-Tutorials#git-switch) and [git restore](https://github.com/twtrubiks/Git-Tutorials#git-restore).

`git checkout -- file` can discard modifications in the working directory:

```cmd
git checkout -- hello.py
```

The command `git checkout -- hello.py` means to undo (discard) all modifications to the hello.py file in the working directory,

returning this file to the state of the last `git commit` or `git add`.

![alt tag](https://i.imgur.com/SrCo4kH.jpg)

Of course, you can also use the `git reset` command to directly revert to a certain commit.

```cmd
git reset --hard xxxxxx
```

```cmd
git reset --hard 201f40604ec3b6fa8
```

## Deletion

There are two situations. One is that you are sure you want to delete the file from the repository. In that case, use the `git rm` command to delete it, and then `git commit`:

```cmd
rm hello.py
git rm hello.py
git commit -m "remove hello.py"
```

![alt tag](https://i.imgur.com/sLMTDX7.jpg)

The other situation is that you deleted it by mistake. You can easily restore the file using `git checkout`:

```cmd
rm hello.py
git checkout -- hello.py
```

![alt tag](https://i.imgur.com/5X2NcfS.jpg)

## Creating and merging branches

Before explaining branches, let me give you a concept.

Usually, during development, everyone creates a branch from **master**, and finally **merges** it back to master.

Why do this? To ensure that everyone is using the latest **master**.

Use the `git branch` command to view the current branch:

```cmd
git branch
```

![alt tag](https://i.imgur.com/SVblXD2.jpg)

First, create a branch, `bug1` branch (the name can be anything), and then switch to the `bug1` branch:

```cmd
git branch bug1
git checkout bug1
```

`git branch bug1` creates a branch named `bug1`.

`git checkout bug1` switches to the branch named `bug1`.

![alt tag](https://i.imgur.com/JtGBHk4.jpg)

The above two commands are equivalent to the following one command:

```cmd
git checkout -b bug1
```

(Here's a little trick, the following command can quickly switch to the previous branch, the concept is the same as `cd -` :exclamation:)

```cmd
git checkout -
```

We make any modifications on the `bug1` branch,

and then merge the work results (note: remember to use `git add` and `git commit` commands after any modification) to the master branch:

```cmd
git checkout master
git merge bug1
```

![alt tag](https://i.imgur.com/pF4xDUE.jpg)

`git checkout master` switches to the branch named master.

The `git merge bug1` command is used to merge the specified branch (`bug1` branch) into the current branch (master).

If it goes very smoothly, "Fast-forward" will appear in the `git merge` message, and the merge speed is very fast.

Of course, not every merge can go smoothly with "Fast-forward". Many times, conflicts will occur.

If the merge is completed successfully, you can delete the (local) `bug1` branch:

```cmd
git branch -d dev
```

![alt tag](https://i.imgur.com/LmKKWxR.jpg)

To discard a branch that has not been merged, you can use `git branch -D branch_name` to force delete (local).

```cmd
git branch -D dev
```

So what if you want to delete a remote branch today? :question:

* [Youtube Tutorial - git delete and view remote branches](https://youtu.be/0JQrT7nfm_c)

```cmd
git push origin --delete {remote_branch}
```

Additionally, `git branch` can also be renamed, and the commit id will not change. The usage is also very simple.

You can refer to the git-branch [documentation](https://git-scm.com/docs/git-branch#git-branch--m). The usage is as follows:

```text
git branch -m <name>
```

The log of the original `b1` branch is as follows:

![alt tag](https://i.imgur.com/b1K1EUy.png)

Now rename the `b1` branch to the `b2` branch:

![alt tag](https://i.imgur.com/Twz5kRm.png)

If you compare it carefully with the previous log, you will find that the commit id of the log does not change.

![alt tag](https://i.imgur.com/qMjqV3Z.png)

## Create a branch using a specific commit id

Sometimes we want to test the state of a certain commit. At this time, we can directly use the commit id to create a branch.

The method is as follows:

```cmd
git checkout -b new_branch <commit id>
```

This will create a branch based on the commit id you specified.

## Create a new branch and push

I believe everyone has seen many branches on GitHub, as shown in the picture below:

![alt tag](https://i.imgur.com/wrIdlzS.jpg)

So how do we create a branch? First, let's look at the picture below:

![alt tag](https://i.imgur.com/3U092a1.jpg)

There is a `v1` branch, and I added a `g.py` and committed it on the branch.

Next, when you **first** `git push`, you will find an error message.

Please use the following command, which is the correct one:

```cmd
git push --set-upstream origin v1
```

You can also use:

```cmd
git push -u origin v1
```

For more detailed instructions, please refer to [https://git-scm.com/docs/git-push#git-push--u](https://git-scm.com/docs/git-push#git-push--u)

![alt tag](https://i.imgur.com/1fuS2VY.jpg)

Next, you can go to the webpage to see (here using Bitbucket as an example), you will find that there is a `v1` branch.

![alt tag](https://i.imgur.com/lOtzsk8.jpg)

If this is the first time you use `git clone`, you will find that you only have the master branch.

At this time, let's first check what other branches are on the remote.

```cmd
git branch -r
```

```cmd
git branch --remote
```

`--remote` or `-r` are both fine.

Suppose there is a branch named `develop` on the remote.

We just need to checkout to that branch.

```cmd
git checkout develop
```

## git switch

[Youtube Tutorial - git switch and git restore tutorial](https://youtu.be/JL_bSOGDR-k)

Please check your current git version first. For update methods, please refer to [git update](https://github.com/twtrubiks/Git-Tutorials#git-%E6%9B%B4%E6%96%B0).

Starting from git version 2.23, `git switch` and `git restore` have been added. These two commands are mainly to more clearly divide functions, mainly to replace `git checkout`.

You can think of `git checkout` = `git switch` + `git restore`.

Official documentation can be found at [git-switch](https://git-scm.com/docs/git-switch)

```cmd
git switch [<options>] (-c|-C) <new-branch> [<start-point>]
```

Switch to an existing branch (if the branch does not exist, the command is invalid)

```cmd
git switch <new-branch>
```

Create `new-branch` and switch to the `new-branch` branch

```cmd
git switch -c <new-branch>
```

`-c` `--create`

`-C` `--force-create`

Create `new-branch` based on commit_id (or the Nth previous commit point) and switch to the `new-branch` branch

```cmd
git switch -c <new-branch> <commit_id>
git switch -c <new-branch> HEAD~2
```

(Here's a little trick, the following command can quickly switch to the previous branch, the concept is the same as `cd -` :smile:)

```cmd
git switch -
```

## git restore

[Youtube Tutorial - git switch and git restore tutorial](https://youtu.be/JL_bSOGDR-k)

Please check your current git version first. For update methods, please refer to [git update](https://github.com/twtrubiks/Git-Tutorials#git-%E6%9B%B4%E6%96%B0).

Starting from git version 2.23, `git switch` and `git restore` have been added. These two commands are mainly to more clearly divide functions, mainly to replace `git checkout`.

You can think of `git checkout` = `git switch` + `git restore`.

Official documentation can be found at [git-restore](https://git-scm.com/docs/git-restore)

The following two commands are the same.

```cmd
git checkout <file>
git restore <file>
```

Restore all files in the current folder

```cmd
git restore .
```

Restore all files ending with `*.py` in the current folder

```cmd
git restore '*.py'
```

If your `git` version is newer, you should find that you have never seen this command before :smile:

![alt tag](https://i.imgur.com/IHqfVrn.png)

```cmd
git restore --staged <file>
```

## git pull

Usually, before starting work or pushing, you will first pull the branch from the remote.

```cmd
git pull
```

If there are conflicts, you must resolve them first.

Here's a supplement on the `-C` parameter. It means to specify the folder path.

Sometimes we may not want to `cd` into the folder first and then pull. At this time, it is very suitable to use it :smile:

```cmd
git [-C <path>] pull
```

Example:

```cmd
cd git_folder
git pull
```

Can be simplified to:

```cmd
git -C git_folder pull
```

## git fetch

You can simply think of **git pull = git fetch + git merge**

Let's first look at the picture below, **git fetch + git merge**

![alt tag](https://i.imgur.com/COuWByw.png)

Then look at this picture **git pull**

![alt tag](https://i.imgur.com/8FGuA75.png)

Isn't it much clearer now!!!

An additional parameter `--prune` is added.

* [Youtube Tutorial - git fetch command prune parameter explanation](https://youtu.be/ZMpMv1P1Q1Q)

The main function of this is to delete invalid branches on the remote.

Sometimes, even though the remote branch has been deleted, when you execute `git branch --remote`, you will find that you can still see those branches (but the branches on the webpage have been removed :sweat:)

This often happens on the pull side (non-working side) machine (if you don't understand what this means, it is recommended to watch the video explanation :smile:)

At this time, you can synchronize the local and remote branches using the following command:

`git fetch --prune`

## git rebase

What is rebase? `git rebase` is to avoid redundant (meaningless) merges!!! First, look at the two pictures below.

Note:

ck = checkout

br = branch

st = status

cm = commit

You can set it yourself.

Picture 1

![alt tag](https://i.imgur.com/mWY0f2J.png)

Picture 2

![alt tag](https://i.imgur.com/QVZc5P5.png)

Which picture do you prefer to look at, Picture 1 or Picture 2? The answer is obvious, it's Picture 1!!

The main purpose of **rebase** is to make the graph look like Picture 1 as much as possible.

It's confusing to just talk about it, so I'll show you a practical example.

First, an example **without using rebase**.

Current branch

![alt tag](https://i.imgur.com/E0ahfnD.png)

![alt tag](https://i.imgur.com/Lb4dB0V.png)

The above explanation: First create a v1 branch, then add and commit.

Suppose someone else has pushed now. The following simulates a pull, adding a commit yourself.

![alt tag](https://i.imgur.com/hFKX4yJ.png)

The above explanation: Add t2.txt on the master branch yourself, and commit (simulating a pull).

Next, switch to the master branch and merge with the v1 branch, and push.

![alt tag](https://i.imgur.com/0sCH2Q1.png)

You will find that the displayed graph is not beautiful, as shown below:

![alt tag](https://i.imgur.com/zbIPdyb.png)

Example of **using rebase**.

The previous parts are basically the same.

![alt tag](https://i.imgur.com/E0ahfnD.png)

![alt tag](https://i.imgur.com/Lb4dB0V.png)

The above explanation: First create a v1 branch, then add and commit.

Suppose someone else has pushed now. The following simulates a pull, adding a commit yourself.

![alt tag](https://i.imgur.com/hFKX4yJ.png)

The above explanation: Add t2.txt on the master branch yourself, and commit (simulating a pull).

***The different part***

![alt tag](https://i.imgur.com/45ZXGiK.png)

The above explanation: First switch to the v1 branch, then use the following command:

```cmd
git rebase master
```

![alt tag](https://i.imgur.com/Lpd9Kjr.png)

The above explanation: Then switch back to the master branch, and use merge to merge the v1 branch, and finally push.

See~ Isn't it much neater and more beautiful?

![alt tag](https://i.imgur.com/1jBI7pw.png)

`git rebase` is to bring back the latest commit from master, and then add the commit of your own branch.

The above is the introduction of `git rebase`.

Another way, just now you had to switch to the v1 branch to execute the command.

If you are now on any branch (like the master branch), you can use the following command:

```cmd
git rebase master v1
```

That is, specify v1 at the end. After execution, it will automatically switch you to the v1 branch.

The result is the same.

In addition, there is another command `git rebase --onto`

```cmd
git rebase --onto <new base-commit> <current base-commit>
```

The concept is actually the same, it's just which new base-commit you want to rebase to.

Just put the current base-commit at the end.

You can view it with `git graph`, or look at the git documentation `git rebase --help`.

## git rebase interactive

When I was young, I always thought that `git rebase` was just to make the commit log look cleaner. But I accidentally discovered that the interactive mode of `git rebase` is super powerful. So, here I will introduce the powerful features of `git rebase` :smirk:

The following are the commands that can be used in `git rebase interactive`. I copied these descriptions from git, and I will show them to you later.

```cmd
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
```

If you want to learn more, please refer to [INTERACTIVE MODE](https://git-scm.com/docs/git-rebase#_interactive_mode).

There is nothing much to say about `pick`, it just uses this commit :smile:

### reword

[Youtube Tutorial - git rebase interactive - reword - PART 1](https://youtu.be/JhY0rR2wQq0)

```cmd
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
```

The following is the official description:

```txt
If you just want to edit the commit message for a commit, replace the command "pick" with the command "reword".
```

The description is already very clear, it is to edit the commit message.

(You cannot modify the commit content, that is, the content of the files)

Suppose, now we have a git log like this:

![alt tag](https://i.imgur.com/6bWnJnK.png)

Commit id `2659f65` has a typo. The correct commit message should be `add c.py`.

So now we need to correct it. Our target commit id is `2659f65`. The command is:

```cmd
git rebase -i <after-this-commit>
```

What does `after-this-commit` mean? :question:

Simply put, you need to select the one before the current commit id.

In this example, our target commit id is `2659f65`, but we must issue the command:

```cmd
git rebase -i f0a761d
```

![alt tag](https://i.imgur.com/d15nGjx.png)

This should be very clear. In short, remember to choose the one before the target commit id.

When you press ENTER, you should see the following picture:

![alt tag](https://i.imgur.com/4ISGcW1.png)

Part A is the target we want to modify, and part B is the description (the stuff I posted for you earlier).

Next, press `i` to enter edit mode, then change the target to `r` or `reword`, and then enter `:wq`.

![alt tag](https://i.imgur.com/zPeHuDa.png)

Then we press ENTER again, and another screen will pop up. At this time, you change the commit message to the correct one, changing `add c.py Typo` to `add c.py`.

![alt tag](https://i.imgur.com/brYbNqy.png)

After entering `:wq`, press ENTER again (done).

![alt tag](https://i.imgur.com/kitKqrm.png)

Let's check the log again (as shown below). It has been successfully modified, and the message has been changed to `add c.py`.

![alt tag](https://i.imgur.com/rWojGIu.png)

There is one thing I want to mention to everyone here, that is, the commit id will change. I will frame the changed part for you to see.

Before modification:

![alt tag](https://i.imgur.com/6i6Wv35.png)

After modification:

![alt tag](https://i.imgur.com/mvj96U2.png)

Simply put, the commit ids after the current commit id will all change (a bit of a tongue twister :sweat_smile:).

Here's a supplement, as long as you use rebase, you will see a picture similar to the one below.

![alt tag](https://i.imgur.com/iiDf44q.png)

`origin/master` refers to the remote repo. It tells you that your current repo is now different from `origin/master`. So, at this time, if you want to push, please use `git push --force-with-lease`.

Someone might ask here, what if I want to modify the first commit? :question:

At this time, you can use:

```cmd
git rebase -i --root
```

### edit

[Youtube Tutorial - git rebase interactive - edit - PART 2](https://youtu.be/TCKjQppHxxQ)

```cmd
# Commands:
# p, pick = use commit
# e, edit = use commit, but stop for amending
```

The following is the official description:

```txt
By replacing the command "pick" with the command "edit", you can tell git rebase to stop after applying that commit, so that you can edit the files and/or the commit message, amend the commit, and continue rebasing.
```

Simply put, `reword` can only modify the commit message, while `edit` can not only modify the commit message but also the content of the files.

Let's look at the picture below first:

![alt tag](https://i.imgur.com/9j0JnKw.png)

This picture clearly shows `add a.py` -> `add b.py` -> `add c.py` -> `add d.py`. Now I want to add something between `add c.py` and `add d.py`, that is, to make it `add a.py` -> `add b.py` -> `add c.py` -> `add c1.py` -> `add d.py`.

You can use `edit` when you want to add `add c1.py`. (I won't go into so much detail below, I'll just get to the point).

First, execute the following command (our target is `a7ed6ff`, so choose its previous commit id, which is `f0a761d`).

```cmd
git rebase -i f0a761d
```

This time we change `pick` to `e` or `edit` (as shown below):

![alt tag](https://i.imgur.com/bKrLIl3.png)

When you press ENTER, you will see the picture below:

![alt tag](https://i.imgur.com/whkCzok.png)

Part A is where you can modify the commit message.

Part B tells you that when you are done modifying (satisfied), you can execute `git rebase --continue`.

We won't do part A, but let's do some processing now (add `c1.py`).

First, we create a `c1.py` file, then `git add c1.py`, and then commit it (as shown below):

![alt tag](https://i.imgur.com/frYBUfT.png)

As I said just now, when you are satisfied, you can execute `git rebase --continue`, and you're done.

![alt tag](https://i.imgur.com/sjnEn0H.png)

Check the log again, it's amazing :satisfied: it was added successfully.

![alt tag](https://i.imgur.com/irECwLH.png)

### squash

[Youtube Tutorial - git rebase interactive - squash fixup - PART 3](https://youtu.be/bfrZrbEHis0)

```cmd
# Commands:
# p, pick = use commit
# s, squash = use commit, but meld into previous commit
```

The following is the official description:

```text
 The suggested commit message for the folded commit is the concatenation of the commit messages of the first commit and of those with the "squash" command,
```

Simply put, if you want to merge multiple commits into one, just use `squash`. (I won't go into so much detail below, I'll just get to the point).

The goal this time is to merge commit id `fc45824` and commit id `a7ed6ff` (as shown below):

![alt tag](https://i.imgur.com/v8XwOTN.png)

First, execute the following command:

```cmd
git rebase -i f0a761d
```

Then you will see the picture below. We change the `pick` of the `fc45824` commit to `s` or `squash`.

(It will merge with its previous one, which is `a7ed6ff`)

![alt tag](https://i.imgur.com/rgWkvVp.png)

(If you want to merge multiple commits, just change them all to `s` or `squash`. Note, there is an order :exclamation: :exclamation:)

Then press ENTER, and you will see the picture below:

![alt tag](https://i.imgur.com/pB6yllA.png)

At this time, it has already merged these two commits. We can enter a new commit message.

Here we enter `add c.py and c1.py`.

![alt tag](https://i.imgur.com/m9E6KUp.png)

Press ENTER again (success).

![alt tag](https://i.imgur.com/X0O7I5H.png)

You can check the log again. We have successfully merged the two commits.

![alt tag](https://i.imgur.com/r53KIev.png)

Both `c.py` and `c1.py` exist, which means we have succeeded :satisfied:

![alt tag](https://i.imgur.com/WhkLDGa.png)

### fixup

[Youtube Tutorial - git rebase interactive - squash fixup - PART 3](https://youtu.be/bfrZrbEHis0)

```cmd
# Commands:
# p, pick = use commit
# f, fixup = like "squash", but discard this commit's log message
```

The following is the official description:

```text
omits the commit messages of commits with the "fixup" command.
```

This is actually very similar to `squash`. Usually, if we want to ignore a commit message but keep the content of the commit, we will use `fixup`.

Goal: Here we want to remove the commit `fc45824` (but keep the content of the commit).

![alt tag](https://i.imgur.com/AFrd0UA.png)

First, execute the following command:

```cmd
git rebase -i f0a761d
```

Change the `pick` of `fc45824` to `f` or `fixup` (as shown below).

![alt tag](https://i.imgur.com/aDH1y1n.png)

(It will remove the commit message of `fc45824`, but keep the content of the commit)

Then ENTER, and rebase successfully.

![alt tag](https://i.imgur.com/BMs2h8r.png)

You can check the log again. We have ignored the `add c1.py` commit.

![alt tag](https://i.imgur.com/bgYJa6T.png)

But both `c.py` and `c1.py` exist (only the commit message is ignored).

![alt tag](https://i.imgur.com/tYrB3F9.png)

Seeing this, everyone can actually think about it. `squash` and `fixup` are very similar.

It's just that `squash` can modify the commit message.

To put it simply, when you just want to ignore a certain commit message, use `fixup`.

When you want to merge commits and modify the commit message, use `squash`.

### exec

[Youtube Tutorial - git rebase interactive - exec drop - PART 4](https://youtu.be/u8imRiiSyzk)

```cmd
# Commands:
# p, pick = use commit
# x, exec = run command (the rest of the line) using shell
```

The following is the official description:

```text
You may want to check that your history editing did not break anything by running a test, or at least recompiling at intermediate points in history by using the "exec" command (shortcut "x")
```

I use this function less often, but I'll still talk about it. Simply put, it can be used to check if your rebase changes have affected the whole thing (use the `exec` command to confirm).

Don't understand? :question: It's okay. Suppose I made a lot of rebase changes today, but I want to confirm if my changes have affected the whole thing. That is, I can run your tests while making changes to confirm that the whole thing is working normally.

Still don't understand? :question: It's okay, I'll use an example to show you.

![alt tag](https://i.imgur.com/iu1bEOw.png)

As shown in the picture above, suppose I want to do some tests during my changes to ensure that my changes will not affect the whole thing.

(Although they are all `pick` here, which means no changes, but for the convenience of explanation, please imagine that there are changes :sweat_smile:)

![alt tag](https://i.imgur.com/2c9ycmS.png)

Part A, `echo "test sucess"`, naturally has no problem.

But part B will have a problem, because there is no `error` command at all.

When the shell has an error during execution, it will stop and let you fix it.

As shown in the picture below, we stopped at the `add c.py` commit, because the next test failed.

![alt tag](https://i.imgur.com/yVB3naC.png)

At this time, we can fix the problem. After fixing it, execute `git rebase --continue`.

![alt tag](https://i.imgur.com/YBD0d9V.png)

I think this function is for you to run your own tests while modifying to ensure that the changes are normal.

### drop

[Youtube Tutorial - git rebase interactive - exec drop - PART 4](https://youtu.be/u8imRiiSyzk)

```cmd
# Commands:
# p, pick = use commit
# d, drop = remove commit
```

The following is the official description:

```text
To drop a commit, replace the command "pick" with "drop", or just delete the matching line.
```

This is much simpler. Remove this commit (including the commit content).

Suppose our log is as follows:

![alt tag](https://i.imgur.com/zz5arVp.png)

The goal this time is to remove the commits `f0a761d`, `980bd9a`, and `1539219`.

First, execute the following command:

```cmd
git rebase -i 8f13aaa
```

Change `pick` to `d` or `drop` (as shown below):

![alt tag](https://i.imgur.com/Goc1LH1.png)

After pressing ENTER, check the log again.

![alt tag](https://i.imgur.com/u7z2Y3U.png)

From the picture above, you can see that we have successfully removed the commits `f0a761d`, `980bd9a`, and `1539219`.

And we also see that the commit content has been removed, only `a.py` is left.

## git pull supplement

Now that we have introduced `git fetch` and `git rebase`, I will add some additional options for `git pull`.

```cmd
git pull [<options>] [<repository> [<refspec>…​]]
```

For more detailed commands, please refer to [https://git-scm.com/docs/git-pull#_options](https://git-scm.com/docs/git-pull#_options).

Here is a simple summary:

```cmd
git pull = git fetch + git merge
git pull --rebase = git fetch + git rebase
```

In [git-rebase](https://github.com/twtrubiks/Git-Tutorials#git-rebase), everyone has already understood that using `git-rebase` can make it more comfortable for code reviewers. So just use `git pull --rebase` (provided you know what you are doing :smile:).

Here I simulate the difference between `git pull` and `git pull --rebase`, and also add the case of conflicts. Because there are many steps, if you want to understand more about its concept, please refer to the following step-by-step tutorial:

[Youtube Tutorial - git pull vs git pull --rebase](https://youtu.be/8h0K-2OaeSk)

The result after using `git pull`, the code reviewer will definitely flip the table (as shown below) :triumph:

Here I also simulated the case of conflicts. You will find that if you use `git pull`, there will be an extra commit (which is "fix conflict" below).

![alt tag](https://i.imgur.com/CNgKR3y.png)

The result after using `git pull --rebase`, the code reviewer will feel warm (as shown below) :innocent:

![alt tag](https://i.imgur.com/RKMo9ue.png)

Here I also simulated the case of conflicts. You will find that if you use `git pull --rebase`, there will not be an extra commit like just now.

The reason is that when we use `git pull --rebase` and cause a conflict, after fixing the conflict content, `git add xxxx`, then we will directly execute `git rebase --continue`.

Suppose you executed `git pull --rebase` today and found it very uncomfortable :fearful:, and want to cancel it.

Just execute `git rebase --abort` to return to the previous state.

Additional tips:

* [Youtube Tutorial - git autostash parameter explanation](https://youtu.be/kg2PyZr7l5k)

Explanation of `--autostash`.

Generally, if we are in the middle of work and suddenly want to directly `git pull --rebase` without committing, the process will be something like this:

```cmd
git stash # Stash the current changes
git pull --rebase
git stash pop # Pop the previous changes from the stash
# If there are conflicts, resolve them
```

But it's a bit annoying to have to execute so many commands every time :sweat:

But you can solve it with a parameter, which is:

`git pull --rebase --autostash`

The above command basically helps you execute the string of things just now.

If there are conflicts, just fix them :smile:

## git-cherry-pick

Watching the video will be clearer. Step-by-step guide to do it yourself [Youtube Tutorial - git-cherry-pick](https://youtu.be/x3UtKUvlDdI)

The `git-cherry-pick` command may be unfamiliar to everyone :confused:

It's okay, let's first look at the [official](https://git-scm.com/docs/git-cherry-pick) description:

```text
git-cherry-pick - Apply the changes introduced by some existing commits
```

Still :question: :question: :question: after reading the official description?

It's okay, I'll assume a scenario (after understanding it, you will understand the purpose of `git-cherry-pick`).

Suppose the log of the master branch is as shown in the picture below:

![alt tag](https://i.imgur.com/cMcn6yE.png)

And there is a v1 branch with a log as shown in the picture below:

![alt tag](https://i.imgur.com/OZ7JLke.png)

Now I want to merge the commit `14dee93 - add d.py` from the v1 branch.

(Because the commit `14dee93` is so great or for some reason only this commit is needed)

In the above situation, it is very suitable to use `git-cherry-pick`. That is to say, I only want a few commits from other branches, not all of them. In other words, it is to pick commits from other branches to use.

After understanding the suitable usage scenario, let's practice it :smirk:

First, I want the commit `14dee93 - add d.py` from the v1 branch.

So I first switch to the master branch, and then execute:

```cmd
git cherry-pick 14dee93
```

If you want to pick many branches at once, you can also do it. Just separate them with spaces.

```cmd
git cherry-pick 14dee93 xxxxxx xxxxxx xxxxxx xxxxx
```

If you want to pick a range of commits at once, you can use the following command:

```cmd
git cherry-pick A^..B
```

(A and B represent your commit ids)

If there are no conflicts, you will see the picture below:

![alt tag](https://i.imgur.com/YITXxMk.png)

Let's look at the master's log again:

![alt tag](https://i.imgur.com/iGEIDZL.png)

You will find that we have successfully taken the commit `14dee93 - add d.py` from the v1 branch and used it. But now its commit id is `ab70429`. This is normal because it needs to be recalculated :smile:

Actually, you will find that `git-cherry-pick` is not as difficult as you imagined :satisfied:

When cherry-picking, it is inevitable to encounter conflicts. Here I will do another example of a conflict.

Suppose the master's log is as follows:

![alt tag](https://i.imgur.com/pttbQ5U.png)

The log in the v1 branch is as follows. I want its commit `3a2f29a - add c.py and print world`.

![alt tag](https://i.imgur.com/RFibHS6.png)

The log in the v2 branch is as follows. I want its commit `553587b - add f.py`.

![alt tag](https://i.imgur.com/I6L2Fwq.png)

Next, we switch back to master and cherry-pick these two commits.

At this time, you will find that it has a conflict :fearful:

![alt tag](https://i.imgur.com/fAtQET0.png)

Use `git status` to check the status. Part A has already taught you how to resolve conflicts.

![alt tag](https://i.imgur.com/J8ZpPng.png)

First, we fix `c.py`, execute `git add c.py`, and then follow part A to execute `git cherry-pick --continue`. At this time, an editor window will pop up.

![alt tag](https://i.imgur.com/giylVAL.png)

After entering the commit message, enter `wq`, and you will see the picture below:

![alt tag](https://i.imgur.com/rA8wMbO.png)

Finally, look at the log again.

![alt tag](https://i.imgur.com/lEP648c.png)

We have successfully merged the commits we want into our master branch :kissing_smiling_eyes:

To learn more about usage, you can refer to the official documentation [https://git-scm.com/docs/git-cherry-pick](https://git-scm.com/docs/git-cherry-pick).

## git revert

Suppose my commit history is A1 -> A2 -> A3 -> A4 -> A5 -> A6

Now I want to go back to the commit A4. At this time, I can use `git revert`!!

First, revert A6

```cmd
git revert A6
```

Then revert A5

```cmd
git revert A5
```

If you look at the current commit history, it will look like this:

A1 -> A2 -> A3 -> A4 -> A5 -> A6 -> A6_revert -> A5_revert

At this time, your commit is actually at the position of A4.

The advantage of using `git revert` is that you can keep the commit history. If you regret it again, you can revert back.

If you want to revert the latest commit, just use HEAD

```cmd
git revert HEAD
```

## Resolving conflicts

When merging, sometimes **conflicts** will be displayed. At this time, you must manually resolve the conflicts before submitting.

Usually, the easiest way for me to encounter conflicts is when using the `pull` command.

![alt tag](https://i.imgur.com/Eph0Vw1.jpg)

Look carefully at this picture. If you use the **pull** command, it will help you **auto-merge** (as shown in the picture, Auto-merging Hello.py).

Then look at CONFLICT (content): Merge conflict in Hello.py, and it also says Automatic merge failed.

This tells you that the Hello.py file has a conflict, and you must manually resolve the conflict.

`git status` can tell us the conflicting files.

![alt tag](https://i.imgur.com/vlVcXn8.jpg)

Open the conflicting file and we will see that Git uses `<<<<<<<`, `=======`, `>>>>>>>` to mark the content of different branches. We modify it and then submit:

![alt tag](https://i.imgur.com/rlPOaxn.jpg)

Usually, we will manually modify the conflicts and then add a commit.

```cmd
git add Hello.py
git commit -m "conflict fixed"
```

### Suppose we want to abandon this merge today, what should we do?

```cmd
git merge --abort
```

or

```cmd
git reset --hard HEAD
```

You can cancel this merge and go back to the state before the merge.

## git stash command

* [Youtube Tutorial - git stash command](https://youtu.be/CN065MNHtMY)

Many times, we are developing a new feature or debugging, and suddenly a feature needs to be fixed urgently.

But you don't want to commit the current situation because it's meaningless. The work is only half done. At this time, the useful command **stash** comes in handy.

For example, suppose we have modified two files, A.py and B.py.

![alt tag](https://i.imgur.com/7xX0T1T.jpg)

And now, suddenly there is a bug that must be dealt with immediately.

But, I haven't finished my work yet~~~~

At this time, you can use the following command:

```cmd
git stash
```

![alt tag](https://i.imgur.com/cYCH8mV.jpg)

If you want to be clearer about the reason for this stash, or what feature is being developed, you can use the following command:

Example:

```cmd
git stash save "I am a comment"
```

```cmd
git stash save -u "feature"
```

Parameter description:

`-u` | `--include-untracked`

`-a` | `--all`

![alt tag](https://i.imgur.com/nGS11Px.jpg)

Next, you can use the `status` command, and you will find that it has become clean.

![alt tag](https://i.imgur.com/Xf53GfM.jpg)

And you can use the following command to view the things in the stash:

```cmd
git stash list
```

![alt tag](https://i.imgur.com/jQPiYiX.jpg)

Then you work hard to solve this bug. After committing, you can use the following command to get the stash back. This command will also delete the stash after getting it back.

```cmd
git stash pop
```

Suppose you have many stashes today. You can specify them as follows (choose the usage you like):

```cmd
git stash pop 0
git stash pop stash@{0}
```

![alt tag](https://i.imgur.com/zVF7no2.jpg)

You will find that the things just now are back~

If you want to get the stash back without deleting it, you can use the following command:

```cmd
git stash apply
```

As shown in the picture below, you can find that the stash is not deleted after being retrieved.

![alt tag](https://i.imgur.com/w3Ip3iW.jpg)

If you just want to delete the temporary storage, you can use the following command:

```cmd
git stash clear
```

From the picture below, you can find that the things in the stash have been deleted by us.

![alt tag](https://i.imgur.com/PvzufbQ.jpg)

If you want to discard a specified stash, you can use (choose the usage you like):

```cmd
git stash drop 0
git stash drop stash@{0}
```

## git tag

[Youtube Tutorial - git tag tutorial](https://youtu.be/azciLlpr3Gs)

View tags

```cmd
git tag
```

![alt tag](https://i.imgur.com/8f6zGfm.png)

Specify keywords

```cmd
git tag -l "v1.*"
```

`-l` `--list`

`git tag` has lightweight tags and annotated tags.

Lightweight tag

If you want to create a lightweight tag, please do not specify `-a`, `-s` (GPG-signed), `-m`.

```cmd
git tag tag_name [commit_id]
```

If you only use `git tag tag_name` without adding the commit id later, the tag will be automatically placed on the current commit id.

Show comments

```cmd
git show v1.1-light
```

Annotated tag

```cmd
git tag -a v1.1 -m "version 1.1"
```

`-a` is the tag name `--annotate`

`-m` represents the description (comment) of the tag

Set a tag on a specified commit

```cmd
git tag -a v1.2 -m "version 1.1" [commit_id]
```

Show comments

```cmd
git show v1.1
```

The difference between a lightweight tag and an annotated tag is whether you can see more details.

An annotated tag has more information.

Lightweight tag is as follows:

![alt tag](https://i.imgur.com/4cUkdyQ.png)

Annotated tag is as follows:

![alt tag](https://i.imgur.com/DQWB1uh.png)

When you execute `git push`, by default, it will not push the tag to the remote.

You need to execute the following command to push the tag to the remote:

```cmd
git push origin [tagname]
```

Push many tags at once (this will push all your tags that are not on the remote).

```cmd
git push origin --tags
```

When others execute `git clone` or `git fetch`, they can get these tags.

Remove local tag

```cmd
git tag -d [tagname]
```

Delete remote tag

```cmd
git push --delete origin [tagname]
```

## git show

Generally, I only use it to see what has been modified in this commit.

```cmd
git show <commit ID>
```

![alt tag](https://i.imgur.com/rjpl8VL.png)

```cmd
git show [<options>] [<object>…​]
```

For other more detailed introductions, please refer to [https://git-scm.com/docs/git-show](https://git-scm.com/docs/git-show)

## git diff

The following is the official description:

```text
 Show changes between commits, commit and working tree, etc
```

Here are a few examples:

The file has not yet entered the staging area (Stage), that is, before executing `git add xxx`.

You can see what modifications have been made.

![alt tag](https://i.imgur.com/nj5Gz5P.jpg)

You can also see the differences between commits.

![alt tag](https://i.imgur.com/JMJ48jO.jpg)

For other more detailed introductions, please refer to [https://git-scm.com/docs/git-diff](https://git-scm.com/docs/git-diff)

## git diff-tree

git-diff-tree - Compares the content and mode of blobs found via two tree objects

Compare the differences between two blobs (commits).

The documentation can be found at [git-diff-tree](https://git-scm.com/docs/git-diff-tree/en)

Let's look at an example directly:

```cmd
git diff-tree -r --no-commit-id --name-status -a --diff-filter=ACDMRT <one commit id> <commit-id to compare> > changes.txt
```

`-r` means Recurse into sub-trees.

`--no-commit-id` This flag suppressed the commit ID output.

`--name-status` Show only the name(s) and status of each changed file.

`--text` `-a` Treat all files as text.

`--diff-filter=[(A|C|D|M|R|T|U|X|B)…​[*]]`

Added (A), Copied (C), Deleted (D), Modified (M), Renamed (R),

have their type (i.e. regular file, symlink, submodule, …​)

changed (T), are Unmerged (U), are Unknown (X),

or have had their pairing Broken (B).

After execution, open `change.txt` and you will see the names of the different files.

```text
M	addons/account/i18n/account.pot
M	addons/account/i18n/ar.po
M	addons/account/i18n/az.po
M	addons/account/i18n/be.po
M	addons/account/i18n/bg.po
M	addons/account/i18n/ca.po
M	addons/account/i18n/cs.po
......
```

## git archive

Continuing the example above, if you want to package the different files between different commits (you don't want to export the whole package because it's too big, you just want to find the different files), you can use the `archive` command. The example is as follows:

```cmd
git archive --format=zip --output=files-diff.zip HEAD $(git diff-tree -r --no-commit-id --name-only --diff-filter=ACMRT <one commit id> <commit-id to compare>)
```

The exported zip file will be the complete files that are different between these two commits.

## git grep

The following is the official description:

```text
git-grep - Print lines matching a pattern
```

Simply put, it can help you find files that match a pattern. For example, if I want to find files whose content contains the pattern "hello", I can execute the following command:

```cmd
git grep "hello"
```

![alt tag](https://i.imgur.com/t5vxvvp.png)

It will show which file and which piece of code uses that pattern.

For other more detailed introductions, please refer to [https://git-scm.com/docs/git-grep](https://git-scm.com/docs/git-grep)

## git clean

Delete untracked files.

`git clean -n`

`-n, --dry-run` Don’t actually remove anything, just show what would be done`

This command tells you which data will be deleted, but it will not actually delete it.

Example is as follows:

```cmd
❯ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test.py

nothing added to commit but untracked files present (use "git add" to track)

❯ git clean -n
Would remove test.py
```

If you execute the following command, it will actually delete it.

`git clean -df`

For detailed instructions, you can use `git clean --help` to view.

Example is as follows:

```cmd
❯ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test.py

nothing added to commit but untracked files present (use "git add" to track)

❯ git clean -df
Removing test.py

❯ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

Do you still remember the `git reset` command introduced earlier? Basically, it can be used together with `git clean`.

`git clean` affects untracked files.

`git reset` affects tracked files.

Combining the above, you can go back to a clean state of a specified commit.

```cmd
git reset --hard HEAD
git clean -df
git status
```

I suggest everyone to operate it yourself.

## git Submodule

Since this content is a bit more, I wrote another article.

* [Youtube Tutorial PART 1 - git Submodule tutorial - how to create submodule](https://youtu.be/IDMWLJCbCGo)

* [Youtube Tutorial PART 2 - git Submodule tutorial - how to update submodule](https://youtu.be/ogZoZOVyAYI)

* [Youtube Tutorial PART 3 - git Submodule tutorial - how to clone submodule](https://youtu.be/f5_O5Iu6pJo)

* [Youtube Tutorial PART 4 - git Submodule tutorial - how to remove submodule](https://youtu.be/imndFN7AvFA)

[git Submodule tutorial :memo:](https://github.com/twtrubiks/Git-Tutorials/blob/master/git_submodule_turorial.md)

## git Subtree

Since this content is a bit more, I wrote another article.

* [Youtube Tutorial PART 1 - git subtree tutorial - how to create subtree](https://youtu.be/kEvgK2gH_vg)

* [Youtube Tutorial PART 2 - git subtree tutorial - how to push subtree](https://youtu.be/Df3zc1VOqN8)

* [Youtube Tutorial PART 3 - git subtree tutorial - how to pull/create subtree](https://youtu.be/dE-D2yrD4ws)

[git subtree tutorial :memo:](https://github.com/twtrubiks/Git-Tutorials/blob/master/git_subtree_turorial.md)

## Other git settings

We have already set `user.name` and `user.email`, but there are many other things that can be set in Git.

Sometimes, we have to put some files (folders) into the Git working directory, but we cannot commit them.

For example, password settings or things generated by the compiler IDE.

Every time `git status` shows red Untracked files, it's usually a bit annoying......

Git has also thought about this problem for us. Just create a special **.gitignore** file in the root directory of the Git working area.

Then enter the names of the files (files) to be ignored, and Git will automatically ignore these files.

Of course, you don't need to write the `.gitignore` file from scratch. GitHub has already prepared some files for us [gitignore](https://github.com/github/gitignore)

The **.gitignore** file can be placed directly under the directory.

![alt tag](https://i.imgur.com/8rHPsII.jpg)

### .gitignore file format example

![alt tag](https://i.imgur.com/W3cxk9r.jpg)

### .gitignore (Temporarily and Permanently)

It is mainly divided into temporary and permanent ignore.

* Temporarily ignore

It is suitable for settings files. Sometimes when we are developing, we will have our own settings.

But this setting is not necessarily needed by everyone. At this time, you can temporarily ignore the changes of this file.

Temporarily ignore a file

```cmd
git update-index --skip-worktree <file>
```

Resume temporarily ignoring a file

```cmd
git update-index --no-skip-worktree <file>
```

* Permanently ignore

Here is a supplementary scenario. Suppose the file has been committed to git today.

But I want to add it to `.gitignore`. What should I do? :question:

If you add the file to `.gitignore`, you will find that it is still not ignored :confused:

![alt tag](https://i.imgur.com/o922paa.png)

At this time, the correct way is to execute the following command first.

```cmd
git rm --cached <file>
```

After execution, commit again (the file will not be deleted from the system, it is just to update the git index).

![alt tag](https://i.imgur.com/RJZ08OQ.png)

At this time, you can try to update the content of the file again, and you will find that it has been successfully ignored :smile:

### git alias

Sometimes I often make typos or can't remember the commands.

If we type `git st` to mean `git status`, that would be great!!!

So we can set it ourselves, so that in the future, typing **git st = git status**
As shown in the picture below, originally `git st` could not be used. After setting it, it can be used.

![alt tag](https://i.imgur.com/4NNasgB.jpg)

```cmd
git config --global alias.br branch
```

![alt tag](https://i.imgur.com/NIc71AO.jpg)

```cmd
git config --global alias.ck checkout
```

```cmd
git config --global alias.sw switch
```

```cmd
git config --global alias.cm commit
```

```cmd
git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative"
```

Turn this long string into an alias, so that in the future, you only need to execute `git lg`.

![alt tag](https://i.imgur.com/IvQLsMR.png)

Someone might ask, where is this configuration file?

Usually, it is under your user. For example, the user of this computer is HJ, so the configuration file will be under **C:\Users\HJ**.

It is a **hidden file .gitconfig**. If you open it, the format is as follows.

![alt tag](https://i.imgur.com/iXjIqv9.jpg)

I wonder if everyone has noticed the `--global` parameter. It means global. If you execute it today:

```cmd
git config alias.stu status
```

It means that it only takes effect in that directory.

So what's the use of this? Imagine a scenario where you want to use a specific email to push under a specific folder, while for other folders, you still use the company's email. At this time, it is very suitable to use this method.

For more information and details, you can use the following command to view:

```cmd
man git-config
```

### git update

```cmd
sudo add-apt-repository ppa:git-core/ppa
sudo apt-get update
sudo apt-get install git
```

![alt tag](https://i.imgur.com/WrQNZln.png)

## Use Git to push to multiple different remotes at once

If GitHub goes down one day, does that mean you can't work? You might say you still have a local copy?

But......more backups are definitely a good thing!! Here I will introduce how to push to multiple different remotes at once.

Here we use [Bitbucket](https://bitbucket.org/product) as an example.

First, use the command below to check:

```cmd
git remote -v
```

![alt tag](https://i.imgur.com/Qb5VHoP.png)

For more instructions on the `git remote` command, you can refer to the official documentation [git-remote](https://git-scm.com/docs/git-remote).

Next, we use the following command to add an `origin` remote:

```cmd
git remote set-url --add origin <url>
```

```cmd
git remote set-url --add origin git@github.com:twtrubiks/test2.git
```

![alt tag](https://i.imgur.com/FKzexVE.png)

Let's use `git remote -v` to check again. You will find that the remote we just added has been added.

![alt tag](https://i.imgur.com/p1q7C4b.png)

Finally, let's push again.

![alt tag](https://i.imgur.com/6VKh8Bz.png)

Look carefully, isn't it pushing to multiple different remotes at once? Very convenient!!

***GitHub***

![alt tag](https://i.imgur.com/JljPJHJ.png)

***Bitbucket***

![alt tag](https://i.imgur.com/rkYHNl4.png)

P.S. The configuration file is in the hidden file ".git" under the folder. There is a `config` file inside.

![alt tag](https://i.imgur.com/41xb8eu.png)

Supplement a few `git remote` commands. It also supports `rename` and `remove`.

The current remote is as follows:

![alt tag](https://i.imgur.com/rr9SE3g.png)

Let's rename the remote. The syntax is as follows:

```text
git remote rename <old> <new>
```

```text
git remote rename origin2 origin
```

After execution, you will find that the remote has been successfully renamed to `origin`.

![alt tag](https://i.imgur.com/ixP1H7Z.png)

Next, let's try `remove`. The syntax is as follows:

```text
git remote remove <name>
```

```text
git remote remove origin
```

Successfully deleted. Now the remote is empty.

![alt tag](https://i.imgur.com/OQFRWDg.png)

Next, let's try to add a remote. The command is as follows:

```text
git remote add [-t <branch>] [-m <master>] [-f] [--[no-]tags] [--mirror=<fetch|push>] <name> <url>
```

```cmd
git remote add origin git@github.com:blue-rubiks/t11.git
```

![alt tag](https://i.imgur.com/cKsiBBs.png)

If we want to modify the url of `origin`, we can use:

```cmd
git remote set-url origin git@blue.github.com:blue-rubiks/t11.git
```

![alt tag](https://i.imgur.com/LJICTNM.png)

## Multiple SSH Keys settings for different github account

* [Youtube Tutorial - Multiple SSH Keys settings for different github account](https://youtu.be/gDxG-4tF7B8)

[Multiple SSH Keys settings for different github account](https://github.com/twtrubiks/Git-Tutorials/blob/master/Multiple_SSH_Keys_settings.md)

## Git-Flow Basic Tutorial and Concepts

* [Git-Flow Tutorials - youtube](https://youtu.be/zXlta66thZY)

* [Git-Flow SmartGit Tutorials - youtube](https://youtu.be/ualXHytifbg)

[Git-Flow Basic Tutorial and Concepts](https://github.com/twtrubiks/Git-Tutorials/tree/master/Git-Flow)

## PR (Pull Request) Tutorial

* [Youtube Tutorial - github PR (Pull Request) tutorial](https://youtu.be/bXOdD-bKfkA) - [Article Quick Link](https://github.com/twtrubiks/Git-Tutorials/tree/master/pr-tutorial#github-pr-pull-request-%E6%95%99%E5%AD%B8)

* [Youtube Tutorial - github CLI PR tutorial - gh](https://youtu.be/AD8X11lq3gQ) - [Article Quick Link](https://github.com/twtrubiks/Git-Tutorials/tree/master/pr-tutorial#github-cli-pr-%E6%95%99%E5%AD%B8)

[PR (Pull Request) Tutorial](https://github.com/twtrubiks/Git-Tutorials/tree/master/pr-tutorial)

## Linux Notes

* [Youtube Tutorial - Linux Tutorial - git ignore file mode (chmod) changes](https://youtu.be/QCh2k903Yak)

Here I will talk about some problems you may encounter when using git on both windows and linux.

First, execute the following command on linux:

```cmd
sudo chmod -R 777 folder
```

git will default it as a change. How to ignore it? Please execute the following command:

```cmd
git config core.fileMode false
```

You can also refer to this article [Git ignore file mode (chmod) changes](https://stackoverflow.com/questions/1580596/how-do-i-make-git-ignore-file-mode-chmod-changes)

### Formatting

`core.autocrlf`

Windows uses both Enter (Carriage Return, abbreviated as CR) and Line Feed (abbreviated as LF) to define a new line.

While Mac and Linux only use one Line Feed (LF) character.

So it will cause problems in cross-platform collaboration.

You can set it like this on windows (meaning LF will be converted to CRLF):

```cmd
git config --global core.autocrlf true
```

Linux or Mac system:

```cmd
git config --global core.autocrlf input
```

With the above settings, CRLF will be preserved on Windows, and LF will be preserved on Mac and Linux and in the repo.

If you want to understand more deeply, you can refer to [Formatting-core.autocrlf](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration#Formatting-and-Whitespace).

### Modify editor

```cmd
git config --global core.editor "vim"
```

## Reference

* [13 Git tips for Git's 13th birthday](https://opensource.com/article/18/4/git-tips)

## Donation

The articles are all original after my own research and internalization. If it has helped you and you want to encourage me, you are welcome to buy me a cup of coffee :laughing:

ECPAY (no membership registration required)

![alt tag](https://payment.ecpay.com.tw/Upload/QRCode/201906/QRCode_672351b8-5ab3-42dd-9c7c-c24c3e6a10a0.png)

[Sponsor Payment](http://bit.ly/2F7Jrha)

O'Pay (membership registration required)

![alt tag](https://i.imgur.com/LRct9xa.png)

[Sponsor Payment](https://payment.opay.tw/Broadcaster/Donate/9E47FDEF85ABE383A0F5FC6A218606F8)

## Sponsor List

[Sponsor List](https://github.com/twtrubiks/Thank-you-for-donate)
