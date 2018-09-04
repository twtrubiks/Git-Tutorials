# git Submodule tutorial :memo:

手把手帶大家動手做 [Youtube Tutorial PART 1 - git Submodule tutorial - how to create submodule](https://youtu.be/IDMWLJCbCGo)，

git Submodule 的官方文件可參考 [git-submodule](https://git-scm.com/docs/git-submodule/)。

在開始介紹前，我們先來談談何時會使用到 git Submodule，

大家一定有遇過這種情境，就是 A repo 依賴 B repo，這邊你可能會問我，

阿為什麼不直接把兩個 repo 變成一個 repo 就好呢 :question:

這樣不是增加遊戲困難度 :question:

有時候，這個 B repo 可能是 github 上一個很多人維護超強的東西，

你不可能自己維護，更何況，不要重造輪子，我們要站上巨人的肩膀上 :kissing_smiling_eyes:

好，現在我們拉回來，當每次我們發現 B repo 有更新時，我們以前的做法

可能就要單獨把他 clone 下來，然後在複製進我們的 A repo 中，

但其實這樣真的太土炮，而且非常沒有效率 :expressionless:

那我們該怎麼辦呢 :question:

有沒有一種東西，可以把它整合，甚至我們執行一個指令，就可以把全部

我們依賴的 repo 都做檢查並且更新，如果是這樣的話，整個流程會更安全，

也更不會出錯:relaxed:

答案是有的:thumbsup:

那就是我們接下來要介紹的 git Submodule，如果你也有上述的使用情境，

那你就更需要學習 git Submodule 了 :flushed:

再更簡單一點的說明，你可以把它想成是一個很大的主 repo，然後裡面依賴

很多 A repo、B repo、C repo 之類，而這些  A repo，B repo，C repo，你就可以

把它想成是 Submodule，這樣是不是更清楚了呢 :grin:

既然了解了使用情境，那我們就來看看它該怎麼使用:satisfied:

## how to create submodule

手把手帶大家動手做 [Youtube Tutorial PART 1 - git Submodule tutorial - how to create submodule](https://youtu.be/IDMWLJCbCGo)，

先介紹一下 repo ，這邊有兩個 repo，分別為 main_project repo 以及 a_project repo，

main_project repo 內容如下，

![alt tag](https://i.imgur.com/mLaKJyX.png)

接著，我們要建立 a_project 為 Submodule，建立 Submodule 的語法如下，

```cmd
git submodule add [<options>] [--] <repository> [<path>]
```

實際範例

```cmd
git submodule add git@blue.github.com:blue-rubiks/a_project.git
```

![alt tag](https://i.imgur.com/bexQ5Op.png)

這時候，你如果觀察資料夾，會發現多出一些東西

![alt tag](https://i.imgur.com/djYEPu9.png)

也可以用 `git status` 觀察，

![alt tag](https://i.imgur.com/I9jFYOb.png)

主要是多了 `.gitmodules` 以及 `a_project`，

可以看一下 `.gitmodules` 的內容，裡面就是 path 和 url

![alt tag](https://i.imgur.com/kk8qfTE.png)

雖然表面上是兩個改動，但實際上卻還有一個改動，

它存在 `main_project/.git/config` 中

![alt tag](https://i.imgur.com/mmyFYAk.png)

為什麼我要特別說這個，因為假如今天你想要移除 submodule，

你就必須到這裡移除和 submodule 相關的內容。

接著一些網路上的教學會說需要再執行以下兩個指令，

```cmd
git submodule init
git submodule update
```

但我自己測試似乎是不需要的 ( 雖然執行了也不會有什麼影響 )，

所以就先記錄就好，不要理它:smirk:

接著就一般 git 的操作後，push 就完成了:smiley:

![alt tag](https://i.imgur.com/8c5ygMn.png)

可以使用 `git submodule status` 查看目前 submodule 的狀態

```cmd
git submodule status
```

![alt tag](https://i.imgur.com/44bW6Bs.png)

push 之後，可以到 github 網頁上看，

會發現在 main_project repo 中的 submodule 有一個小圖示，

並且有一個 commit id，

![alt tag](https://i.imgur.com/K0Z5tAa.png)

而這個 commit id，就是 a_project repo 中的 commit id，

![alt tag](https://i.imgur.com/rcyWCGW.png)

學習完了如何建立 Submodule，接下來來看看如何更新 Submodule。

## how to update submodule

手把手帶大家動手做 [Youtube Tutorial PART 2 - git Submodule tutorial - how to update submodule](https://youtu.be/ogZoZOVyAYI)，

假設 a_project repo 也是我們自己維護的，當我們對它更新時，會發生什麼事情:question:

如果你進入 a_project repo 中，你會發現它其實就是一個我們常見的 git repo，

可以正常的 commit 以及 push，

![alt tag](https://i.imgur.com/1REbrbK.png)

**只是你從外面 ( 也就是 main_project repo ) 看到的是像一種參照而已**，

上面這句話很重要，因為我們現在更新了 a_project repo ，可是 main_project 並不

知道它有任何更新，切回 main_project repo 中，你會發現確實有更動，

![alt tag](https://i.imgur.com/jlPgz8P.png)

所以這時候就必須要執行一般的 git 操作並且 push，

![alt tag](https://i.imgur.com/bM8Ow3O.png)

這樣才算是成功，最後這一步驟 **很重要**，有些人會忘記，如果你沒有加上這步驟，

你的 main_project repo 就不知道  a_project repo 有做修改，儘管它是參照的概念，

還是需要此步驟。

剛剛我們是自己改動 a_project repo，現在另一種情境，是別人改動 a_project repo，

那這時候，我們如何更新 Submodule 呢:question:

剛剛說過如果我們進去 a_project repo 中，它就像一個正常的 git 一樣，

所以依照這個原則，

我只要進去 a_project repo 中，並切執行 `git pull` 即可，如下圖，

( 為了方便，我直接去 github 網頁端新增一個檔案，模擬有人更新 repo )

![alt tag](https://i.imgur.com/M9noUKg.png)

但是，因為現在是只有一個 Submodule ，如果你有 N 個 Submodule 呢 ?

這樣我相信會非常麻煩，因為要一個一個更新:sob:

所以，比較好的方法應該是使用以下指令一次更新，

``` cmd
git submodule update --remote
```

更多詳細的 update 可參考 [git-submodule-update](https://git-scm.com/docs/git-submodule#git-submodule-update--init--remote-N--no-fetch--no-recommend-shallow-f--force--checkout--rebase--merge--referenceltrepositorygt--depthltdepthgt--recursive--jobsltngt--ltpathgt82308203)，

`--remote` 的更多說明可以參考 [官方的說明](https://git-scm.com/docs/git-submodule#git-submodule---remote)，

![alt tag](https://i.imgur.com/m2ICwPY.png)

可是這時候你如果切到 a_project repo 你會發現它竟然 **HEAD detached** 了:confused:

![alt tag](https://i.imgur.com/JHMn26S.png)

其實這是正常的，因為默認的行為會將它 checkout 到最新的 commit id 上，

以這個範例 `HEAD detached at 066d0db` 來說，

就是執行了 `git checkout '066d0db'`，所以我們要修正它，

修正方法如下圖，

![alt tag](https://i.imgur.com/VfwxJW4.png)

簡單說就是要建立一個分支 ，然後再回到 master merge 該 ( `066d0db` ) 分支。

但這樣步驟真的有點多:sweat_smile:

所以更簡單的方法，可以直接使用以下指令，

```cmd
git submodule update --remote --merge
```

`--merge` 的 [官方說明](https://git-scm.com/docs/git-submodule#git-submodule-merge) 如下

```text
the commit recorded in the superproject will be merged into the current branch in the submodule.
```

![alt tag](https://i.imgur.com/0YmQoP4.png)

或

```cmd
git submodule update --remote --rebase
```

`--rebase` 的 [官方說明](https://git-scm.com/docs/git-submodule#git-submodule-rebase) 如下

```text
the current branch of the submodule will be rebased onto the commit recorded in the superproject.
```

![alt tag](https://i.imgur.com/MHLvL8T.png)

這種作法更方便，也解決了 **HEAD detached** 的問題 :thumbsup:

## how to clone submodule

手把手帶大家動手做 [Youtube Tutorial PART 3 - git Submodule tutorial - how to clone submodule](https://youtu.be/f5_O5Iu6pJo)，

這邊教大家如何 clone Submodule 的專案，執行一般的 clone 指令，

```cmd
git clone git@github.com:blue-rubiks/main_project.git
```

這時候我們看一下資料夾，

![alt tag](https://i.imgur.com/aiTpngo.png)

的確有將 a_project repo 一起 clone 下來，但不要高興的太早，

因為，你如果進去看這些資料夾查看，你會發現它的內容都是空的:sob:

![alt tag](https://i.imgur.com/xZuY1tm.png)

這時候，我們要先 init submodule，

```cmd
git submodule init
```

![alt tag](https://i.imgur.com/bK6IzKW.png)

執行之後，它會將 `.gitmodules` 中的 url 寫入 `.git/config` 裡面，

![alt tag](https://i.imgur.com/vknhZHR.png)

這時候，submodule 都設定好了，

只需要再執行 update ( update 會依照 `.git/config` 裡面的設定更新  )，

指令如下，

```cmd
 git submodule update --recursive
```

以下為 `--recursive` 官方說明

```text
If --recursive is specified, this command will recurse into the registered submodules, and update any nested submodules within.
```

![alt tag](https://i.imgur.com/SJFZW0U.png)

成功將 submodule 的內容 clone 下來了:smile:

![alt tag](https://i.imgur.com/G9BXL77.png)

上面的兩段指令，也可以合併成一段，

```cmd
git submodule update --init --recursive
```

如果我們一開始就知道我們要 clone 的專案本身就有包含 submodule，

可以直接執行以下指令，

```cmd
git clone --recurse-submodules git@github.com:blue-rubiks/main_project.git
```

一次就完成全部的部分，包含 init 以及更新 submodule:satisfied:

詳細說明可參考 [git-clone---recurse-submodulesltpathspec](https://git-scm.com/docs/git-clone#git-clone---recurse-submodulesltpathspec)，

但通常我們應該是不會一開始就知道這個專案有包含 submodule。

### how to remove submodule

手把手帶大家動手做 [Youtube Tutorial PART 4 - git Submodule tutorial - how to remove submodule](https://youtu.be/imndFN7AvFA)，

要移除 submodule 的步驟比較多，這邊教大家如何移除，

```cmd
git submodule deinit a_project
```

![alt tag](https://i.imgur.com/YcUK6gU.png)

其實 deinit 就是刪除 `.git/config` 裡面的 submodule 相關設定，

![alt tag](https://i.imgur.com/Ek30GqW.png)

接著打開 `.gitmodules` 移除相關的設定，在這邊因為我們只有一個 submodule，

所以直接將 `.gitmodules` 刪除即可。

( 如果只要刪除特定的 submodule，就進去刪除相關的部分 )

接著使用 git rm 指令，詳細用法可參考 [git-rm](https://git-scm.com/docs/git-rm)，

```cmd
git rm --cached a_project
```

![alt tag](https://i.imgur.com/YVHYuDE.png)

如果有加上 `--cached` ，本地端的 submodule repo 會被保留，所以

如果沒有要保留，可以不加上 `--cached`，將會把本地端的 submodule repo 刪除。

接著再移除 `.git/modules/a_project`，

```cmd
rm -rf .git/modules/a_project
```

接著就 `git add` 以及  `git commit`

![alt tag](https://i.imgur.com/LHCpjtg.png)

最後在把空的 a_project 資料夾刪除

```cmd
rm -rf a_project
```

步驟雖然多了點，但其實不難:smirk:

### Synchronizes  Submodule

詳細可參考 [git-submodule-sync](https://git-scm.com/docs/git-submodule#git-submodule-sync--recursive--ltpathgt82308203)

以下為官方說明

```text
Synchronizes submodules' remote URL configuration setting to the value specified in .gitmodules.
```

有時候如果 Submodule 的 remote url 有變更的時候，就需要使用此指令更新。

## Donation

文章都是我自己研究內化後原創，如果有幫助到您，也想鼓勵我的話，歡迎請我喝一杯咖啡:laughing:

![alt tag](https://i.imgur.com/LRct9xa.png)

[贊助者付款](https://payment.opay.tw/Broadcaster/Donate/9E47FDEF85ABE383A0F5FC6A218606F8)

## License

MIT license
