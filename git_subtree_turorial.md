[English Version](git_subtree_turorial_en.md)

# git subtree tutorial :memo:

手把手帶大家動手做 [Youtube Tutorial PART 1 - git subtree tutorial - how to create subtree](https://youtu.be/kEvgK2gH_vg)

還記得之前和大家介紹過 [git Submodule tutorial 📝](https://github.com/twtrubiks/Git-Tutorials/blob/master/git_submodule_turorial.md) 這個指令嗎 :question:

忘記得趕快去複習一下吧 :smirk:

今天我要再來介紹一個類似功能的指令，名稱叫做 **git-subtree**，如果你用 git-subtree 和 git submodule

去 google，你會發現蠻多人拿這兩個來比較的，然後都說什麼 git-subtree 比較推薦之類的，但我這邊先

不下結論，結論在最後面，我先帶大家來了解他怎麼使用。

## 簡介

我先用兩句話來描述 git submodule 和 git subtree 的差異，

***git submodule 是 link 的概念，而 git subtree 則是 copy的概念***

( 如果你看不懂，建議先去閱讀之前我介紹的 Submodule 的 [文章](https://github.com/twtrubiks/Git-Tutorials/blob/master/git_submodule_turorial.md) 吧 )


git subtree 的指令沒有很多，主要指令如下，

```text
'git subtree' add   -P <prefix> <commit>
'git subtree' pull  -P <prefix> <repository> <refspec...>
'git subtree' push  -P <prefix> <repository> <refspec...>
'git subtree' merge -P <prefix> <commit>
'git subtree' split -P <prefix> [OPTIONS] [<commit>]
```

更多詳細內容可參考 [git-subtree](https://github.com/apenwarr/git-subtree/blob/master/git-subtree.txt) 文件。

## 教學

### how to create git subtree

先介紹一下 repo ，這邊有兩個 repo，分別為 main_project_subtree
repo 以及 a_project_subtree repo，

先把 main_project_subtree repo clone 下來，

```cmd
git clone git@github.com:blue-rubiks/main_project_subtree.git
```

main_project_subtree repo log 如下，

![alt tag](https://i.imgur.com/I6i93rr.png)

接下來，要加入 subtree ( 也就是 a_project_subtree )，使用以下指令

```cmd
git subtree add --prefix=a_project_subtree --squash git@github.com:blue-rubiks/a_project_subtree.git master
```

or

```cmd
git subtree add -P a_project_subtree --squash git@github.com:blue-rubiks/a_project_subtree.git master
```

`--prefix` option [文件](https://github.com/apenwarr/git-subtree/blob/master/git-subtree.txt) 說明如下，

```text
-P <prefix>::
--prefix=<prefix>::
	Specify the path in the repository to the subtree you
	want to manipulate.  This option is mandatory
	for all commands.
```

簡單說，prefix 就是指定一個目錄。

`--squash` option [文件](https://github.com/apenwarr/git-subtree/blob/master/git-subtree.txt) 說明如下，

```text
With '--squash', imports only a single commit from the subproject, rather than its entire history.
```

也就是說，如果沒有使用 `--squash`，會將 a_project_subtree 的 log ( 歷史訊息 ) 全部顯示出來

( 請有 log 會變很長又有點亂的心理準備 :scream: )，

但通常我們不太需要顯示全部的 log ( 尤其是依賴的 repo )，所以記得加上 `--squash` option，

這樣的話，就會將全部的 log 合成一個 log

( 其實是兩個，因為還會有一個 merge 的 log :smiley: )

![alt tag](https://i.imgur.com/aUSe38E.png)

main_project_subtree repo log 會變成如下，會多兩個 log，

![alt tag](https://i.imgur.com/NS0aB4B.png)

如果你覺得以上指令實在太長了，可以拆成兩步驟，先執行，

```cmd
git remote add a_project_subtree git@github.com:blue-rubiks/a_project_subtree.git
```

更多詳細資料可參考 [git-remote](https://git-scm.com/docs/git-remote)。

然後執行

```cmd
git subtree add -P a_project_subtree --squash a_project_subtree master
```

其實就是將 remote url 變成 a_project_subtree 而已 :thumbsup:


### how to push git subtree

[Youtube Tutorial PART 2 - git subtree tutorial - how to push subtree](https://youtu.be/Df3zc1VOqN8)

現在的 main_project_subtree 基本上已經將 a_project_subtree 整個 copy 過來了，就算現在

a_project_subtree remote repo 被刪除也沒關係 ( 因為是 copy 過來的 )，而且 developer 甚至

不需要知道有 a_project_subtree 的存在，直接使用一般的 git 操作即可，也就是說，現在

a_project_subtree 就像是在 main_project_subtree 裡面的一個目錄一樣。

如果你修改了 a_project_subtree ，並且執行 git push，在 main_project_subtree 中可以看到

資料被修改，但是在 a_project_subtree 中會看不到修改，因為還沒有 push 到 a_project_subtree，

那該如何 push 到 a_project_subtree 上呢 :question:

可以使用以下指令

```cmd
git subtree push -P a_project_subtree a_project_subtree master
```

或是

```cmd
git subtree push -P a_project_subtree git@github.com:blue-rubiks/a_project_subtree.git master
```

update a_project_subtree，

![alt tag](https://i.imgur.com/QsyZEcK.png)

接著 push 改變到 a_project_subtree repo，

![alt tag](https://i.imgur.com/F8SJ2pn.png)

注意 `4/4 (2)` 這個，他每次都會重新 ( 重源頭 ) 計算，所以如果你一直增加 a_project_subtree 的 commit，

每次 push 到 a_project_subtree 的速度會越來越慢，該如何解決 :question:

後面會介紹 :smirk:

![alt tag](https://i.imgur.com/PnpAmqU.png)

如果你要 push 改變到 main_project_subtree，直接執行一般的 `git push` 操作就行了，

![alt tag](https://i.imgur.com/2T9Bn13.png)

到這邊我們休息一下 :relaxed:

在簡介的時候我們說過 **git submodule 是 link 的概念，而 git subtree 則是 copy 的概念**，所以如果你

仔細看 main_project_subtree 以及 a_project_subtree 的 log，你會發現他們是不一樣的 ( 因為 git subtree

有自己的策略 )，而之前介紹的 git submodule 則會有相同的 commit id 以及 submodule 的 commit link。

### how to pull git subtree

[Youtube Tutorial PART 3 - git subtree tutorial - how to pull/create subtree](https://youtu.be/dE-D2yrD4ws)

如果今天我們要更新 a_project_subtree repo 可以使用以下指令，

```cmd
git subtree pull -P a_project_subtree a_project_subtree master
```

或是

```cmd
git subtree pull -P a_project_subtree git@github.com:blue-rubiks/a_project_subtree.git master
```

執行後，應該會跳出 `fatal: refusing to merge unrelated histories` 失敗的訊息，

![alt tag](https://i.imgur.com/hcqBtrK.png)

會出現這個的原因是因為我們在前面有執行 `git subtree add -P a_project_subtree --squash `

中的 `--squash`，所以 pull 的時候也必須加上，也就是如下，

![alt tag](https://i.imgur.com/AoOcXFa.png)

這樣才可以成功 pull :smile:

### git subtree split

split 這個指令比較特別，在這邊我提一下，在前面的 [how to push git subtree](https://github.com/twtrubiks/Git-Tutorials/blob/master/git_subtree_turorial.md#how-to-push-git-subtree) 部分有提到 `4/4 (2)`

這個是他每次都會重新計算，所以如果你一直增加 commit，push 速度會越來越慢的這個問題，

而 split 可以解決這個問題，他會從一個最新的點開始計算，不用每次都重頭計算 :smile:

先來看一下 [文件](https://github.com/apenwarr/git-subtree/blob/master/git-subtree.txt)，`--rejoin` option

```text
If you do all your merges with '--squash', don't use
'--rejoin' when you split, because you don't want the
subproject's history to be part of your project anyway.
```

我們在 `git subtree add` 以及 `git subtree pull` 都有使用 `--squash`，所以

如果再使用`--rejoin` option 的話，會導致 a_project_subtree 的 history log 都

被 clone 回來，所以我們必須再加上 `--ignore-joins option`，指令如下，

```cmd
git subtree split --rejoin --prefix=a_project_subtree --ignore-joins
```

![alt tag](https://i.imgur.com/owS1Nz7.png)

這樣就完成 split 了，當我們如果有改動 a_project_subtree，`4/4 (2)` 這個就會重最新的點開始計算，

不會每次都重頭計算，導致 push 速度越來越慢 :satisfied:

## 結論

介紹完了 subtree ，一定要來說說我對 subtree 以及 submodule 的看法 :laughing:

在 submodule 中執行 init 以及如果要移除掉 submodule 時，步驟都比較繁瑣，

相對 subtree 來說，subtree 簡單很多，因為對 developer 來說，他就像一個

目錄一樣，就算今天 subtree 的 remote repo 被刪除也不擔心 :smiley:

但是我相信大家一定也發現了，使用 subtree 的時候，我們如果要切換 branch

並沒有想像中的容易 ( 在 submodule 中，我們可以進到依賴的 repo 中，然後

像操作一般的 git 使用 `git checkout` 來切換 branch，但在 subtree 中卻無法

這樣使用，因為他是整個 copy 過來的，不像 submodule 那樣是 link 的概念。 )

所以如果有切分支 ( 你依賴的 repo )，建議還是使用 submodule 會比較方便，

另外一個點是，我覺得使用 subtree 時，會讓 log 變得有點亂 :weary:，不像

submodule 那樣清楚很多 :smile:

而且 subtree 的侵略性比較強 ( commit id 都會改變)，大家在使用時，要多了解

一下，雖然 subtree 指令看似只有幾個，但是整體使用下來，還是很多細節要注意 :sweat_smile:

## Donation

文章都是我自己研究內化後原創，如果有幫助到您，也想鼓勵我的話，歡迎請我喝一杯咖啡 :laughing:

![alt tag](https://i.imgur.com/LRct9xa.png)

[贊助者付款](https://payment.opay.tw/Broadcaster/Donate/9E47FDEF85ABE383A0F5FC6A218606F8)

## License

MIT license
