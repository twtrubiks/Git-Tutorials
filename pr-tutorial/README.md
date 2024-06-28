# PR (Pull Request) 教學

先來說說甚麼時候可以使用 PR (Pull Request),

* 情境一

你在網路上看到一個很棒的專案, 然後你很想要為這個專案盡一份心力, 這時候就你就可以透過 PR 這個機制,

通常你不會有這個專案的權限, 所以一定是 Fork 這個專案到自己的 repo 下修改 -> 修改完後推回自己的分支

-> 再對對應的原專案發 PR(注意對方的以及自己的 branch ) -> 等作者測試覺得沒問題後合併進主分支

-> 恭喜你對社群盡了一分心力:smile:

* 情境二

公司也可以使用 PR 的模式進行多人開發, 但通常在這個情況下你都會有專案的權限(和情境一不同), 所以你就

不需要 Fork, 直接開 branch 後對特定的 branch(可能是 develop) 發 PR 即可.


**情境一和情境二基本上都是一樣的概念, 唯一差別就是是否有 repo 的權限, 如果沒有就需要 Fork.**

今天主要會透過 情境二 和大家簡單介紹 PR 的操作.

* [Youtube Tutorial - github PR (Pull Request) 教學](https://youtu.be/bXOdD-bKfkA) - [文章快速連結](https://github.com/twtrubiks/Git-Tutorials/tree/master/pr-tutorial#github-pr-pull-request-%E6%95%99%E5%AD%B8)

* [Youtube Tutorial - github CLI PR 教學](https://youtu.be/AD8X11lq3gQ) - [文章快速連結](https://github.com/twtrubiks/Git-Tutorials/tree/master/pr-tutorial#github-cli-pr-%E6%95%99%E5%AD%B8)

## github PR (Pull Request) 教學

使用 [Git-Flow 基本教學](https://github.com/twtrubiks/Git-Tutorials/tree/master/Git-Flow) 的概念來做教學,

為了簡單一點, 在這邊就只有 main(master), develop, feature 分支.

今天有個需求來了, 我首先先從 develop 開一個 feature 分支,

假設做完了需求, 就把 feature 分支 push 上去, 然後開始發 PR.

現在要對 develop 發 PR, 要發的分支是 feature. (如下圖)

![alt tag](https://i.imgur.com/XfTq0hc.png)

選好之後就可以按下 Create pull request,

接著你會看到專案下有一個 PR,

![alt tag](https://i.imgur.com/ad8BM6T.png)

這時候可能是技術主管(依照各公司的流程)看到這個 PR, 如果沒有甚麼問題,

可以選擇要使用哪種的 Merge pull request 的方式.

![alt tag](https://i.imgur.com/JX9pQDU.png)

有三種 Merge pull request 可以選擇,

* Create a Merge Commit

基本上這個就是一般的 merge, 但我通常不喜歡這個, 因為會有無意義的 merge commit.

* Squash and Merge

這個就是假如你有一個功能, 總共使用了 10 個 commit 才完成這個功能, 但是這些 commit

其實都沒有太重要的資訊, 這時候你可以選擇使用 Squash 的方式, 把這 10 個 commit 合併成

一個 commit. (其他的 commit 會變成你的 message).

* Rebase and Merge

這個和 Create a Merge Commit 的差別就是他不會有無意義的 merge commit, 他有移花接木

的概念, 你的分支上有 3個 commit, 使用這方法合併後就是會多出 3個 commit.

至於要使用哪一種, 就看各公司的需求了:smile:

決定好 Merge pull request 的方式後就可以直接按下了, 你會發現他顯示 Merged,

並且也可選擇是否刪除該分支以及 revert 這個 PR.

![alt tag](https://i.imgur.com/ZuJ2eh1.png)

基本上整個流程就是這樣, develop 向 main 發送 PR 也是一樣的概念.

## github CLI PR 教學

如果你有看前面的文章, 你就會覺得很麻煩:expressionless:

因為每次都要手動去網頁上點, 工程師肯定要使用 CLI,

今天我就來教大家這個 [github CLI](https://cli.github.com/):laughing:

連 github 的網頁都不需要開:satisfied:

首先是安裝方法

[https://github.com/cli/cli/blob/trunk/docs/install_linux.md](https://github.com/cli/cli/blob/trunk/docs/install_linux.md)

接著是登入的方法 [gh_auth_login](https://cli.github.com/manual/gh_auth_login)

```cmd
gh auth login
```

選擇你要的登入方式即可.

順便一提, github CLI 的文件寫的很好, 大家可以參考他的文件玩玩看 [GitHub CLI document](https://cli.github.com/manual/).

接下來, 就要來體驗 github CLI 的強大了:satisfied:

現在有一個 `feature_cli` 分支, 當 push 分支之後,

(溫馨提醒:exclamation::exclamation: 要發一個 PR, 這個 branch 一定要 push 到 remote)

(也就是說, 你沒辦法去發送一個 PR 只存在 local 端但卻不存在 remote 端)

(如果你只想要 PR 特定的 commit, 請使用 `git checkout -b [branch] [commit_id]` 再發送 PR)

就可以透過 github CLI 發 PR, 要向 develop 分支發 PR, 指令如下

文件可參考 [https://cli.github.com/manual/gh_pr_create](https://cli.github.com/manual/gh_pr_create)

```cmd
gh pr create --base develop --head feature_cli
```

如果你目前就在 `feature_cli` 分支底下, 也可以只輸入

```cmd
gh pr create --base develop
```

成功透過 github CLI 發送 PR

![alt tag](https://i.imgur.com/sZF3SuH.png)

github 上面也確實有這個 PR

![alt tag](https://i.imgur.com/7atBIzY.png)

也可以搭配其中的指令

```cmd
gh pr create --base dev -a @me -l bug -r twtrubiks
```

`-a` 代表指定這個 pr 給自己

`-l` label 設定為 bug

`-r` 設定 reviews 為 twtrubiks

除了發 PR 之外, 也可以透過 github CLI 接受 PR, 指令如下

文件可參考 [https://cli.github.com/manual/gh_pr_merge](https://cli.github.com/manual/gh_pr_merge)

```cmd
gh pr merge -s 2
```

參數說明,

`-m` Create a Merge Commit.

`-s` Squash and Merge.

`-r` Rebase and Merge.

數字 2 則代表要合併的 PR 編號.

![alt tag](https://i.imgur.com/hedvtIi.png)

github 上面確實已經合併這個 PR

![alt tag](https://i.imgur.com/h6akTEd.png)

也可以建立 issue [gh_issue_create](https://cli.github.com/manual/gh_issue_create)

```cmd
gh issue create -a @me -l bug
```

`-a` 代表指定這個 issue 給自己

`-l` label 設定為 bug

還有非常多的指令, 就不一一介紹給大家了, 大家請自行研究:relaxed:

基本上, github CLI 功能是非常強大的:smile:

### 其他

gh 預設的 editor 是 nano, 以下指令為修改成 vim

```cmd
gh config set editor vim
```
