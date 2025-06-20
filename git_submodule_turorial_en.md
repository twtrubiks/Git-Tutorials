# git Submodule tutorial :memo:

[English Version](git_submodule_turorial_en.md)

Step-by-step guide [Youtube Tutorial PART 1 - git Submodule tutorial - how to create submodule](https://youtu.be/IDMWLJCbCGo).

The official documentation for git Submodule can be found at [git-submodule](https://git-scm.com/docs/git-submodule/).

Before we start, let's talk about when to use git Submodule.

Everyone must have encountered a situation where repo A depends on repo B. Here you might ask me,

why not just combine the two repos into one? :question:

Isn't that just making the game harder? :question:

Sometimes, this B repo might be a super powerful thing on GitHub maintained by many people.

You can't maintain it yourself, and what's more, don't reinvent the wheel, we should stand on the shoulders of giants :kissing_smiling_eyes:

Okay, now let's get back to it. When we find that B repo has been updated, our previous method

might be to clone it separately and then copy it into our A repo.

But this is really too primitive and very inefficient :expressionless:

So what should we do? :question:

Is there something that can integrate it, or even a command we can run to check and update all

the repos we depend on? If so, the whole process would be safer and less prone to errors :relaxed:

The answer is yes :thumbsup:

That's what we're going to introduce next, git Submodule. If you have the above usage scenario,

then you need to learn git Submodule even more :flushed:

To put it more simply, you can think of it as a large main repo that depends on

many A repos, B repos, C repos, etc. And these A repos, B repos, C repos, you can

think of them as Submodules. Isn't that clearer? :grin:

Now that we understand the usage scenario, let's see how to use it :satisfied:

## how to create submodule

Step-by-step guide [Youtube Tutorial PART 1 - git Submodule tutorial - how to create submodule](https://youtu.be/IDMWLJCbCGo).

First, let me introduce the repos. There are two repos here, main_project repo and a_project repo.

The content of main_project repo is as follows:

![alt tag](https://i.imgur.com/mLaKJyX.png)

Next, we want to create a_project as a Submodule. The syntax for creating a Submodule is as follows:

```cmd
git submodule add [<options>] [--] <repository> [<path>]
```

Actual example:

```cmd
git submodule add git@blue.github.com:blue-rubiks/a_project.git
```

![alt tag](https://i.imgur.com/bexQ5Op.png)

At this point, if you look at the folder, you will find that some things have been added.

![alt tag](https://i.imgur.com/djYEPu9.png)

You can also observe with `git status`.

![alt tag](https://i.imgur.com/I9jFYOb.png)

Mainly, `.gitmodules` and `a_project` have been added.

You can look at the content of `.gitmodules`. It contains the path and url.

![alt tag](https://i.imgur.com/kk8qfTE.png)

Although it seems like two changes on the surface, there is actually another change.

It exists in `main_project/.git/config`.

![alt tag](https://i.imgur.com/mmyFYAk.png)

Why do I specifically mention this? Because if you want to remove a submodule today,

you must go here to remove the content related to the submodule.

Next, some online tutorials will say that you need to execute the following two commands again:

```cmd
git submodule init
git submodule update
```

But I tested it myself and it seems unnecessary (although executing it won't have any effect).

So just record it for now and ignore it :smirk:

Then, after the general git operations, push and you're done :smiley:

![alt tag](https://i.imgur.com/8c5ygMn.png)

You can use `git submodule status` to view the current status of the submodule.

```cmd
git submodule status
```

![alt tag](https://i.imgur.com/44bW6Bs.png)

After pushing, you can go to the GitHub webpage to see.

You will find that there is a small icon in the submodule in the main_project repo.

And there is a commit id.

![alt tag](https://i.imgur.com/K0Z5tAa.png)

And this commit id is the commit id in the a_project repo.

![alt tag](https://i.imgur.com/rcyWCGW.png)

After learning how to create a Submodule, let's see how to update a Submodule.

## how to update submodule

Step-by-step guide [Youtube Tutorial PART 2 - git Submodule tutorial - how to update submodule](https://youtu.be/ogZoZOVyAYI).

Suppose the a_project repo is also maintained by ourselves. What happens when we update it? :question:

If you enter the a_project repo, you will find that it is actually a common git repo.

You can commit and push normally.

![alt tag](https://i.imgur.com/1REbrbK.png)

**It's just that from the outside (that is, the main_project repo), you see it as a kind of reference.**

The above sentence is very important, because we have now updated the a_project repo, but main_project does not

know that it has any updates. Switch back to the main_project repo, and you will find that there are indeed changes.

![alt tag](https://i.imgur.com/jlPgz8P.png)

So at this time, you must perform general git operations and push.

![alt tag](https://i.imgur.com/bM8Ow3O.png)

This is considered successful. This last step is **very important**. Some people will forget it. If you don't add this step,

your main_project repo will not know that the a_project repo has been modified. Although it is a reference concept,

this step is still needed.

Just now we modified the a_project repo ourselves. Now another scenario is that someone else modified the a_project repo.

At this time, how do we update the Submodule? :question:

As I said just now, if we go into the a_project repo, it's like a normal git.

So according to this principle,

I just need to go into the a_project repo and execute `git pull`, as shown below.

(For convenience, I directly added a file on the GitHub webpage to simulate someone updating the repo)

![alt tag](https://i.imgur.com/M9noUKg.png)

But, because there is only one Submodule now, what if you have N Submodules?

I believe it will be very troublesome because you have to update them one by one :sob:

So, a better way is to use the following command to update them all at once:

``` cmd
git submodule update --remote
```

For more detailed updates, please refer to [git-submodule-update](https://git-scm.com/docs/git-submodule#git-submodule-update--init--remote-N--no-fetch--no-recommend-shallow-f--force--checkout--rebase--merge--referenceltrepositorygt--depthltdepthgt--recursive--jobsltngt--ltpathgt82308203).

For more information on `--remote`, you can refer to the [official documentation](https://git-scm.com/docs/git-submodule#git-submodule---remote).

![alt tag](https://i.imgur.com/m2ICwPY.png)

But at this time, if you switch to the a_project repo, you will find that it is **HEAD detached** :confused:

![alt tag](https://i.imgur.com/JHMn26S.png)

This is actually normal, because the default behavior will check it out to the latest commit id.

Take this example `HEAD detached at 066d0db`.

It is to execute `git checkout '066d0db'`, so we need to fix it.

The correction method is as shown below:

![alt tag](https://i.imgur.com/VfwxJW4.png)

Simply put, you need to create a branch, and then go back to master and merge that (`066d0db`) branch.

But this step is really a bit much :sweat_smile:

So a simpler method is to directly use the following command:

```cmd
git submodule update --remote --merge
```

The [official documentation](https://git-scm.com/docs/git-submodule#git-submodule-merge) for `--merge` is as follows:

```text
the commit recorded in the superproject will be merged into the current branch in the submodule.
```

![alt tag](https://i.imgur.com/0YmQoP4.png)

or

```cmd
git submodule update --remote --rebase
```

The [official documentation](https://git-scm.com/docs/git-submodule#git-submodule-rebase) for `--rebase` is as follows:

```text
the current branch of the submodule will be rebased onto the commit recorded in the superproject.
```

![alt tag](https://i.imgur.com/MHLvL8T.png)

This method is more convenient and also solves the **HEAD detached** problem :thumbsup:

## how to clone submodule

Step-by-step guide [Youtube Tutorial PART 3 - git Submodule tutorial - how to clone submodule](https://youtu.be/f5_O5Iu6pJo).

Here's how to clone a Submodule project. Execute the general clone command:

```cmd
git clone git@github.com:blue-rubiks/main_project.git
```

At this time, let's look at the folder.

![alt tag](https://i.imgur.com/aiTpngo.png)

It did clone the a_project repo together, but don't be too happy too soon.

Because, if you go in and look at these folders, you will find that their contents are empty :sob:

![alt tag](https://i.imgur.com/xZuY1tm.png)

At this time, we need to init the submodule first.

```cmd
git submodule init
```

![alt tag](https://i.imgur.com/bK6IzKW.png)

After execution, it will write the url in `.gitmodules` into `.git/config`.

![alt tag](https://i.imgur.com/vknhZHR.png)

At this time, the submodule is all set up.

You just need to execute update again (update will update according to the settings in `.git/config`).

The command is as follows:

```cmd
 git submodule update --recursive
```

The following is the official documentation for `--recursive`:

```text
If --recursive is specified, this command will recurse into the registered submodules, and update any nested submodules within.
```

![alt tag](https://i.imgur.com/SJFZW0U.png)

Successfully cloned the content of the submodule :smile:

![alt tag](https://i.imgur.com/G9BXL77.png)

The above two commands can also be combined into one:

```cmd
git submodule update --init --recursive
```

If we know from the beginning that the project we want to clone contains submodules,

we can directly execute the following command:

```cmd
git clone --recurse-submodules git@github.com:blue-rubiks/main_project.git
```

Complete all parts at once, including init and updating submodules :satisfied:

For detailed instructions, please refer to [git-clone---recurse-submodulesltpathspec](https://git-scm.com/docs/git-clone#git-clone---recurse-submodulesltpathspec).

But usually we probably won't know from the beginning that this project contains submodules.

### how to remove submodule

Step-by-step guide [Youtube Tutorial PART 4 - git Submodule tutorial - how to remove submodule](https://youtu.be/imndFN7AvFA).

The steps to remove a submodule are a bit more. Here's how to remove it:

```cmd
git submodule deinit a_project
```

![alt tag](https://i.imgur.com/YcUK6gU.png)

In fact, `deinit` is to delete the submodule related settings in `.git/config`.

![alt tag](https://i.imgur.com/Ek30GqW.png)

Next, open `.gitmodules` and remove the related settings. Here, because we only have one submodule,

we can just delete `.gitmodules`.

(If you only want to delete a specific submodule, go in and delete the relevant parts)

Next, use the `git rm` command. For detailed usage, please refer to [git-rm](https://git-scm.com/docs/git-rm).

```cmd
git rm --cached a_project
```

![alt tag](https://i.imgur.com/YVHYuDE.png)

If `--cached` is added, the local submodule repo will be preserved. So

if you don't want to preserve it, you can omit `--cached`, which will delete the local submodule repo.

Next, remove `.git/modules/a_project`.

```cmd
rm -rf .git/modules/a_project
```

Then `git add` and `git commit`.

![alt tag](https://i.imgur.com/LHCpjtg.png)

Finally, delete the empty a_project folder.

```cmd
rm -rf a_project
```

The steps are a bit more, but it's not difficult :smirk:

### Synchronizes Submodule

For details, please refer to [git-submodule-sync](https://git-scm.com/docs/git-submodule#git-submodule-sync--recursive--ltpathgt82308203)

The following is the official documentation:

```text
Synchronizes submodules' remote URL configuration setting to the value specified in .gitmodules.
```

Sometimes if the remote url of the Submodule has changed, you need to use this command to update it.

## Donation

The articles are all original after my own research and internalization. If it has helped you and you want to encourage me, you are welcome to buy me a cup of coffee :laughing:

![alt tag](https://i.imgur.com/LRct9xa.png)

[Sponsor Payment](https://payment.opay.tw/Broadcaster/Donate/9E47FDEF85ABE383A0F5FC6A218606F8)

## License

MIT license
