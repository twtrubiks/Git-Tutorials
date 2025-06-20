# git subtree tutorial :memo:

[English Version](git_subtree_turorial_en.md)

Step-by-step guide [Youtube Tutorial PART 1 - git subtree tutorial - how to create subtree](https://youtu.be/kEvgK2gH_vg)

Do you remember the [git Submodule tutorial 📝](https://github.com/twtrubiks/Git-Tutorials/blob/master/git_submodule_turorial.md) command I introduced before? :question:

If you've forgotten, go review it now :smirk:

Today I'm going to introduce another command with a similar function, called **git-subtree**. If you google `git-subtree` and `git submodule`, you'll find that many people compare the two, and they all say things like `git-subtree` is more recommended. But I won't draw a conclusion here. The conclusion is at the end. I'll first show you how to use it.

## Introduction

I'll first use two sentences to describe the difference between `git submodule` and `git subtree`.

***`git submodule` is a concept of a link, while `git subtree` is a concept of a copy***

(If you don't understand, I suggest you first read the [article](https://github.com/twtrubiks/Git-Tutorials/blob/master/git_submodule_turorial.md) I introduced about Submodule)

There are not many commands for `git subtree`. The main commands are as follows:

```text
'git subtree' add   -P <prefix> <commit>
'git subtree' pull  -P <prefix> <repository> <refspec...>
'git subtree' push  -P <prefix> <repository> <refspec...>
'git subtree' merge -P <prefix> <commit>
'git subtree' split -P <prefix> [OPTIONS] [<commit>]
```

For more detailed content, please refer to the [git-subtree](https://github.com/apenwarr/git-subtree/blob/master/git-subtree.txt) documentation.

## Tutorial

### how to create git subtree

First, let me introduce the repos. There are two repos here, `main_project_subtree` repo and `a_project_subtree` repo.

First, clone the `main_project_subtree` repo.

```cmd
git clone git@github.com:blue-rubiks/main_project_subtree.git
```

The log of `main_project_subtree` repo is as follows:

![alt tag](https://i.imgur.com/I6i93rr.png)

Next, to add a subtree (which is `a_project_subtree`), use the following command:

```cmd
git subtree add --prefix=a_project_subtree --squash git@github.com:blue-rubiks/a_project_subtree.git master
```

or

```cmd
git subtree add -P a_project_subtree --squash git@github.com:blue-rubiks/a_project_subtree.git master
```

The `--prefix` option [documentation](https://github.com/apenwarr/git-subtree/blob/master/git-subtree.txt) is as follows:

```text
-P <prefix>::
--prefix=<prefix>::
	Specify the path in the repository to the subtree you
	want to manipulate.  This option is mandatory
	for all commands.
```

Simply put, `prefix` is to specify a directory.

The `--squash` option [documentation](https://github.com/apenwarr/git-subtree/blob/master/git-subtree.txt) is as follows:

```text
With '--squash', imports only a single commit from the subproject, rather than its entire history.
```

That is to say, if you don't use `--squash`, the entire log (history message) of `a_project_subtree` will be displayed.

(Please be prepared for the log to become very long and a bit messy :scream:).

But usually we don't need to display the entire log (especially for dependent repos), so remember to add the `--squash` option.

In this way, the entire log will be combined into one log.

(Actually two, because there will be another merge log :smiley:)

![alt tag](https://i.imgur.com/aUSe38E.png)

The log of `main_project_subtree` repo will become as follows, with two more logs.

![alt tag](https://i.imgur.com/NS0aB4B.png)

If you think the above command is too long, you can split it into two steps. First, execute:

```cmd
git remote add a_project_subtree git@github.com:blue-rubiks/a_project_subtree.git
```

For more detailed information, please refer to [git-remote](https://git-scm.com/docs/git-remote).

Then execute:

```cmd
git subtree add -P a_project_subtree --squash a_project_subtree master
```

It's just changing the remote url to `a_project_subtree` :thumbsup:

### how to push git subtree

[Youtube Tutorial PART 2 - git subtree tutorial - how to push subtree](https://youtu.be/Df3zc1VOqN8)

Now `main_project_subtree` has basically copied the entire `a_project_subtree`. Even if the `a_project_subtree` remote repo is deleted now, it doesn't matter (because it was copied). And the developer doesn't even need to know that `a_project_subtree` exists. They can just use the general git operations. That is to say, now `a_project_subtree` is like a directory inside `main_project_subtree`.

If you modify `a_project_subtree` and execute `git push`, you can see the data is modified in `main_project_subtree`, but you won't see the modification in `a_project_subtree` because it hasn't been pushed to `a_project_subtree` yet.

So how to push to `a_project_subtree`? :question:

You can use the following command:

```cmd
git subtree push -P a_project_subtree a_project_subtree master
```

or

```cmd
git subtree push -P a_project_subtree git@github.com:blue-rubiks/a_project_subtree.git master
```

update `a_project_subtree`,

![alt tag](https://i.imgur.com/QsyZEcK.png)

Then push the changes to the `a_project_subtree` repo.

![alt tag](https://i.imgur.com/F8SJ2pn.png)

Note `4/4 (2)`. It will be recalculated every time (from the source). So if you keep adding commits to `a_project_subtree`, the speed of pushing to `a_project_subtree` will become slower and slower. How to solve this? :question:

I will introduce it later :smirk:

![alt tag](https://i.imgur.com/PnpAmqU.png)

If you want to push changes to `main_project_subtree`, just execute the general `git push` operation.

![alt tag](https://i.imgur.com/2T9Bn13.png)

Let's take a break here :relaxed:

In the introduction, we said that **`git submodule` is a concept of a link, while `git subtree` is a concept of a copy**. So if you look closely at the logs of `main_project_subtree` and `a_project_subtree`, you will find that they are different (because `git subtree` has its own strategy). And the `git submodule` introduced before will have the same commit id and submodule commit link.

### how to pull git subtree

[Youtube Tutorial PART 3 - git subtree tutorial - how to pull/create subtree](https://youtu.be/dE-D2yrD4ws)

If we want to update the `a_project_subtree` repo today, we can use the following command:

```cmd
git subtree pull -P a_project_subtree a_project_subtree master
```

or

```cmd
git subtree pull -P a_project_subtree git@github.com:blue-rubiks/a_project_subtree.git master
```

After execution, you should get a `fatal: refusing to merge unrelated histories` failure message.

![alt tag](https://i.imgur.com/hcqBtrK.png)

The reason for this is that we executed `git subtree add -P a_project_subtree --squash` with `--squash` before. So when pulling, we must also add it, as follows:

![alt tag](https://i.imgur.com/AoOcXFa.png)

This way you can pull successfully :smile:

### git subtree split

The `split` command is a bit special. I'll mention it here. In the previous [how to push git subtree](https://github.com/twtrubiks/Git-Tutorials/blob/master/git_subtree_turorial.md#how-to-push-git-subtree) section, I mentioned `4/4 (2)`. This is because it recalculates every time, so if you keep adding commits, the push speed will become slower and slower.

And `split` can solve this problem. It will start calculating from the latest point, instead of recalculating from the beginning every time :smile:

Let's first look at the [documentation](https://github.com/apenwarr/git-subtree/blob/master/git-subtree.txt), the `--rejoin` option:

```text
If you do all your merges with '--squash', don't use
'--rejoin' when you split, because you don't want the
subproject's history to be part of your project anyway.
```

We used `--squash` in `git subtree add` and `git subtree pull`. So if we use the `--rejoin` option again, it will cause the history log of `a_project_subtree` to be cloned back. So we must add the `--ignore-joins` option. The command is as follows:

```cmd
git subtree split --rejoin --prefix=a_project_subtree --ignore-joins
```

![alt tag](https://i.imgur.com/owS1Nz7.png)

This completes the split. When we have changes to `a_project_subtree`, `4/4 (2)` will start calculating from the latest point, and will not recalculate from the beginning every time, which causes the push speed to become slower and slower :satisfied:

## Conclusion

After introducing `subtree`, I must talk about my views on `subtree` and `submodule` :laughing:

In `submodule`, executing `init` and removing a submodule are more cumbersome.

Compared to `subtree`, `subtree` is much simpler, because for a developer, it is like a directory. Even if the remote repo of the `subtree` is deleted today, there is no need to worry :smiley:

But I believe everyone has also discovered that when using `subtree`, it is not as easy as imagined to switch branches (in `submodule`, we can go into the dependent repo and use `git checkout` to switch branches like operating a general git, but in `subtree`, we cannot use it this way because it is copied over, unlike `submodule` which is a link concept).

So if you have to switch branches (of your dependent repo), it is recommended to use `submodule` which is more convenient.

Another point is that I think using `subtree` will make the log a bit messy :weary:, unlike `submodule` which is much clearer :smile:

And `subtree` is more aggressive (the commit id will change). When you use it, you need to understand it more. Although `subtree` seems to have only a few commands, there are still many details to pay attention to when using it as a whole :sweat_smile:

## Donation

The articles are all original after my own research and internalization. If it has helped you and you want to encourage me, you are welcome to buy me a cup of coffee :laughing:

![alt tag](https://i.imgur.com/LRct9xa.png)

[Sponsor Payment](https://payment.opay.tw/Broadcaster/Donate/9E47FDEF85ABE383A0F5FC6A218606F8)

## License

MIT license
