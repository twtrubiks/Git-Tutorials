# Git-Flow Basic Tutorial :memo:

[English Version](README_en.md)

[Git-Flow Tutorials - youtube](https://youtu.be/zXlta66thZY)

[Git-Flow SmartGit Tutorials - youtube](https://youtu.be/ualXHytifbg)

Before you start to understand Git-Flow, it is recommended that you have a basic understanding of Git.

You can refer to the [Git-Tutorials GIT Basic Usage Tutorial](https://github.com/twtrubiks/Git-Tutorials) I wrote before.

## What is Git-Flow

There are many commands in Git. If you use Git-Flow, you will have some extra features.

But these features are just combinations of basic functions. To put it simply,

it's the concept of A = B + C + D. Of course, you don't have to worry about memorizing extra commands.

There is a GUI interface (there are many sets to use, I use [SmartGit](http://www.syntevo.com/smartgit/)), and it is very convenient.

## Why use Git-Flow

When you are using Git by yourself, it must be very cool. You can decide how to commit or

how to merge, or even which branch to develop on. But

what if it's a multi-person collaborative development? Everyone has their own habits, wouldn't that

be chaos? So Git-Flow was born.

## Git-Flow is not a new technology, it is just a specification

Many people, when they first see Git-Flow, will think, wow! What is this thing? It's so trendy.

But it is just **a specification**, not a new technology. When a whole

team follows a certain workflow, problems are less likely to occur.

Git-Flow is a set of specifications. If you or your company are very familiar with Git,

you can also define your own Flow. Not following Git-Flow

will not cause any conflicts at all.

## Git-Flow Model

 In Git-Flow, there are two main branches:

***Master***

This branch is very stable and is production-ready at all times. It contains the latest release, which is the source code of the product. When anyone uses your product, the first thing they see is master. **We cannot make any commits directly on the master branch, we can only merge back from Release or Hotfix**.

***Develop***

The development branch. The develop branch is branched from the master branch. This (develop) branch provides integration of different upcoming release features. So this branch may be unstable (have bugs). Usually, we don't commit directly on this branch either, but merge features in through merging.

Master and Develop are two very important branches. In theory, these two branches should be well protected to avoid accidental deletion.

In addition to the **Master** and **Develop** branches, Git-Flow also provides other branches:

***Feature***

Feature development. This branch is branched from the develop branch and will eventually be merged back into the develop branch. For example, suppose there are two features, A and B, being developed by two people. These two people will respectively branch out two branches, A and B, from the develop branch. When they are finished, they will merge back to develop.

***Release***

When we think that develop is already a very stable version, we will enter the release. This branch is branched from the develop branch. Usually, we will do a full test and pre-launch preparation (release version record) on this branch. After completing the release, we will merge back to master and develop.

***Hotfix***

This branch is branched from the master branch. Usually, it is already online, but suddenly a very urgent bug is found. At this time, we will open a Hotfix to fix the bug. After completion, we will merge back to master and develop.

## Using SmartGit to complete Git-Flow

There are many similar GUI interfaces. You can find one that suits you. I will use [SmartGit](http://www.syntevo.com/smartgit/) for the introduction here.

### Installing SmartGit

Please go to [SmartGit](http://www.syntevo.com/smartgit/) to download the one that matches your operating system.

There should be no problems with the installation. The place to pay more attention to is that if you are a non-commercial version,

please choose non-commercial (as shown below). If it is a commercial version, please purchase a license.

![](http://i.imgur.com/Qo6iy0l.jpg)

Set some things to complete.

![](http://i.imgur.com/thRWcvv.jpg)

After entering SmartGit, please select the project first, and then we click the Git-Flow icon (as shown below).

![](http://i.imgur.com/MbJPEIF.jpg)

Usually, we will choose **Full** for Git-Flow Type, which is the complete branch.

![](http://i.imgur.com/xnUn9vS.jpg)

You will find that the two main branches in the lower left corner have appeared.

![](http://i.imgur.com/XfWWByZ.jpg)

To add any Feature or Release, you can click the Git-Flow icon.

![](http://i.imgur.com/0147G33.jpg)

For more detailed introduction, please refer to

[Git-Flow SmartGit Tutorials - youtube](https://youtu.be/ualXHytifbg)

## Reference

* [gitflow](https://github.com/nvie/gitflow)

## Donation

The articles are all original after my own research and internalization. If it has helped you and you want to encourage me, you are welcome to buy me a cup of coffee :laughing:



[Sponsor Payment](https://payment.opay.tw/Broadcaster/Donate/9E47FDEF85ABE383A0F5FC6A218606F8)

## License

MIT license
