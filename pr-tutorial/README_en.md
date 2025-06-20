# PR (Pull Request) Tutorial

[English Version](README_en.md)

First, let's talk about when you can use a PR (Pull Request).

* Scenario 1

You see a great project on the internet and you really want to contribute to it. At this time, you can use the PR mechanism.

Usually, you won't have permission for this project, so you must Fork the project to your own repo for modification -> After modification, push it back to your own branch

-> Then send a PR to the corresponding original project (pay attention to the other party's and your own branch) -> Wait for the author to test and feel that there is no problem before merging into the main branch

-> Congratulations on contributing to the community :smile:

* Scenario 2

The company can also use the PR model for multi-person development, but usually in this case you will have project permissions (different from scenario 1), so you

don't need to Fork. Just open a branch and send a PR to a specific branch (maybe develop).


**Scenario 1 and Scenario 2 are basically the same concept. The only difference is whether you have repo permissions. If not, you need to Fork.**

Today, I will mainly use Scenario 2 to briefly introduce the operation of PR.

* [Youtube Tutorial - github PR (Pull Request) tutorial](https://youtu.be/bXOdD-bKfkA) - [Article Quick Link](https://github.com/twtrubiks/Git-Tutorials/tree/master/pr-tutorial#github-pr-pull-request-%E6%95%99%E5%AD%B8)

* [Youtube Tutorial - github CLI PR tutorial](https://youtu.be/AD8X11lq3gQ) - [Article Quick Link](https://github.com/twtrubiks/Git-Tutorials/tree/master/pr-tutorial#github-cli-pr-%E6%95%99%E5%AD%B8)

## github PR (Pull Request) tutorial

Using the concept of [Git-Flow Basic Tutorial](https://github.com/twtrubiks/Git-Tutorials/tree/master/Git-Flow) for teaching.

To make it simpler, there are only main(master), develop, and feature branches here.

Today, a requirement has come up. I will first open a feature branch from develop.

Assuming the requirement is done, I will push the feature branch up and start sending a PR.

Now I want to send a PR to develop. The branch to be sent is feature. (As shown below)

![alt tag](https://i.imgur.com/XfTq0hc.png)

After selecting, you can press Create pull request.

Then you will see a PR under the project.

![alt tag](https://i.imgur.com/ad8BM6T.png)

At this time, it may be the technical lead (depending on the company's process) who sees this PR. If there are no problems,

you can choose which type of Merge pull request to use.

![alt tag](https://i.imgur.com/JX9pQDU.png)

There are three types of Merge pull request to choose from:

* Create a Merge Commit

This is basically a normal merge, but I usually don't like it because there will be meaningless merge commits.

* Squash and Merge

This is for when you have a feature that took a total of 10 commits to complete, but these commits

don't actually have too much important information. At this time, you can choose to use the Squash method to merge these 10 commits into

one commit. (The other commits will become your message).

* Rebase and Merge

The difference between this and Create a Merge Commit is that it will not have meaningless merge commits. It has the concept of grafting.

If you have 3 commits on your branch, after merging with this method, there will be 3 more commits.

As for which one to use, it depends on the needs of each company :smile:

After deciding on the Merge pull request method, you can press it directly. You will see that it shows Merged.

And you can also choose whether to delete the branch and revert this PR.

![alt tag](https://i.imgur.com/ZuJ2eh1.png)

Basically, the whole process is like this. The concept of develop sending a PR to main is the same.

## github CLI PR tutorial

If you have read the previous articles, you will feel that it is very troublesome :expressionless:

Because you have to manually click on the webpage every time. Engineers must use the CLI.

Today I will teach you this [github CLI](https://cli.github.com/) :laughing:

You don't even need to open the GitHub webpage :satisfied:

First is the installation method:

[https://github.com/cli/cli/blob/trunk/docs/install_linux.md](https://github.com/cli/cli/blob/trunk/docs/install_linux.md)

Next is the login method [gh_auth_login](https://cli.github.com/manual/gh_auth_login)

```cmd
gh auth login
```

Just choose the login method you want.

By the way, the documentation for github CLI is very well written. You can refer to its documentation and play with it [GitHub CLI document](https://cli.github.com/manual/).

Next, let's experience the power of github CLI :satisfied:

Now there is a `feature_cli` branch. After pushing the branch,

(Friendly reminder :exclamation: :exclamation: To send a PR, this branch must be pushed to the remote)

(That is to say, you cannot send a PR that only exists locally but not on the remote)

(If you only want to PR a specific commit, please use `git checkout -b [branch] [commit_id]` and then send the PR)

You can send a PR through github CLI. To send a PR to the develop branch, the command is as follows:

The documentation can be found at [https://cli.github.com/manual/gh_pr_create](https://cli.github.com/manual/gh_pr_create)

```cmd
gh pr create --base develop --head feature_cli
```

If you are currently on the `feature_cli` branch, you can also just enter:

```cmd
gh pr create --base develop
```

Successfully sent a PR through github CLI.

![alt tag](https://i.imgur.com/sZF3SuH.png)

There is indeed this PR on GitHub.

![alt tag](https://i.imgur.com/7atBIzY.png)

You can also use some of its commands:

```cmd
gh pr create --base dev -a @me -l bug -r twtrubiks
```

`-a` means to assign this pr to yourself

`-l` sets the label to bug

`-r` sets the reviewer to twtrubiks

In addition to sending PRs, you can also accept PRs through github CLI. The command is as follows:

The documentation can be found at [https://cli.github.com/manual/gh_pr_merge](https://cli.github.com/manual/gh_pr_merge)

```cmd
gh pr merge -s 2
```

Parameter description:

`-m` Create a Merge Commit.

`-s` Squash and Merge.

`-r` Rebase and Merge.

The number 2 represents the PR number to be merged.

![alt tag](https://i.imgur.com/hedvtIi.png)

This PR has indeed been merged on GitHub.

![alt tag](https://i.imgur.com/h6akTEd.png)

You can also create an issue [gh_issue_create](https://cli.github.com/manual/gh_issue_create)

```cmd
gh issue create -a @me -l bug
```

`-a` means to assign this issue to yourself

`-l` sets the label to bug

There are many other commands, so I won't introduce them one by one. Please study them yourself :relaxed:

Basically, the github CLI function is very powerful :smile:

### Others

The default editor for `gh` is nano. The following command changes it to vim:

```cmd
gh config set editor vim
