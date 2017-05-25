# Git-Tutorials 基本使用教學  :memo:

因為小弟覺得這東西蠻有趣的，所以就簡單寫個教學文，順便記錄一下:memo:，希望能幫助想學的人:smile:

如果教學有誤再請糾正:sweat_smile:

基本使用指令以及安裝可參考小弟之前拍的影片 [github基本教學 - 從無到有](https://www.youtube.com/watch?v=py3n6gF5Y00)

影片教學包含如何產生 **SSH key**

如果步驟正確且沒出錯誤，可以在路徑下找到 **.ssh資料夾**，裡面有 **id_rsa** 以及 **id_rsa.pub** 兩個檔案，

這兩個就是 SSH Key， **id_rsa是私鑰** ，不能洩露出去， **id_rsa.pub是公鑰** ，可以很放心的告訴任何人。

安裝完 Git 之後，要做的第一件事情就是去設定自己的名字和信箱

```cmd
git config --global user.name "twtrubiks"
git config --global user.email "twtrubiks@gmail.com"
```

可以輸入以下來確認是否輸入成功

```cmd
git config --global user.name
git config --global user.email
```

![alt tag](http://i.imgur.com/5mpS7Ij.jpg)

Git 設定資料查看，可執行以下指令 ( 文章末會有較詳細的教學 )：

```cmd
git config --list
```

## git init 指令

初始化 git

```cmd
git init
```

也可以指定資料夾

```cmd
git init <directory>
```

## git clone 指令

複製如圖位置網址 ( 不要複製我的哦~ 複製你自己的 )
![alt tag](http://i.imgur.com/EJ5JNjt.jpg)

git clone ( 複製的網址 ) SSH / HTTPS

```cmd
git clone git@github.com:twtrubiks/test.git
```

第一次會出現 SSH 警告，選 YES 即可。

如圖 ( 下載成功 )，在你的下載路徑下就會多出一個資料夾
![alt tag](http://i.imgur.com/iIkTlqf.jpg)

## git status 指令

```cmd
git status
```

可以讓我們觀看目前的 repository ( repo 容器 )。

![alt tag](http://i.imgur.com/5Gt98Vh.jpg)

意思是目前你的工作區是乾淨的。

## 工作區與暫存區 ( Stage )

git add 意思是把要送出的文件放到暫存區 ( Stage ) ，

然後執行

git commit 就可以把暫存區 ( Stage ) 裡所有修改的內容送到目前的分支上。

一旦送出 ( git commit ) 後，如果你又沒有對工作區做任何修改，那麼工作區就是"乾淨"的。

git commit -m "xxxxx" 指令，-m 後面輸入的內容是本次修改 ( 送出 ) 的說明，

盡量輸入一眼就可以看出這次送出修改了什麼的內容
( 方便以後回去觀看能快速了解此次 commit 修改了什麼 )。

以下 demo 為在一個資料夾內新增一個 Hello.py 檔案

然後使用 git status 觀看目前的 repository ( repo 容器 )，你會看到 Hello.py 未被追蹤，如下圖

![alt tag](http://i.imgur.com/dvj1DQh.jpg)

可以使用如下指令

```cmd
git add Hello.py
```

接著再使用

git commit -m "文字"

```cmd
git commit -m "add Hello.py"
```

再使用 git status，你會發現工作區變乾淨了。如下圖

![alt tag](http://i.imgur.com/6VrieNb.jpg)

補充，如果只有輸入

```cmd
git commit
```

![alt tag](http://i.imgur.com/yZxKGTU.jpg)

這時會跳出編輯視窗

![alt tag](http://i.imgur.com/htNQ0dJ.jpg)

這時可以按鍵盤的 **Ins鍵** ( 或按鍵盤上的 **英文字 i** ) 即可輸入文字

![alt tag](http://i.imgur.com/NFy16dp.jpg)

輸入完先按 **Esc鍵** ，按完後底下的 INSERT 會消失，接著直接打 **:wq** ，再按 enter 就會儲存並離開了。

更多參數可參考 [https://git-scm.com/docs/git-commit](https://git-scm.com/docs/git-commit) 說明。

**如何修改最後一次的commit呢 ?**

有時候我們 commit 完之後，才發現自己的 commit 內容手殘打錯了

這時候可以使用如下指令，他會跳出編輯視窗給你編輯你上一次的 commit 內容。

```cmd
git commit --amend
```

又或是我們 commit 完之後，才發現自己漏了幾個檔案沒有 add 進去

這時候可以使用如下指令

```cmd
git commit -m "init commit"
git add missing_file.py
git commit --amend
```

如上狀況為當我 git commit -m "init commit" 之後，

我發現我漏掉了 **missing_file.py** 這個檔案 ( commit 前忘記 add 進去 ) ，

這時候就可以使用 git commit --amend 來修改最後一次的 commit 。

有時候我們會為了方便，直接使用下面的指令一次加入全部的檔案

```cmd
git add .
```

但是加完後發現其實有些檔案是不需要 add 進入的，這時候就可以使用如下指令去取消 add

```cmd
git reset HEAD <file>
```

範例，路徑下有 A.py 以及 B.py 這兩個檔案，然後我使用 **git add .** 加入，
![alt tag](http://i.imgur.com/0S7TcEB.jpg)

但加入完我發現其實 B.py 我還沒有要 add 進入，所以我這時候就可以使用 **git reset HEAD B.py** 去還原。

![alt tag](http://i.imgur.com/3iAyEEx.jpg)

## git push 指令

```cmd
git push
```

將程式 push 到 github ( or bitbucket 之類 )上 , 如下圖

![alt tag](http://i.imgur.com/d61Pau6.jpg)

## 版本控制 - 歷史記錄

```cmd
git log
```

按 **小寫q** 可退出

![alt tag](http://i.imgur.com/j11afCP.jpg)

如果覺得版面太雜，可以使用下列指令

```cmd
git log --pretty=oneline
```

按 **小寫q** 可退出

![alt tag](http://i.imgur.com/jz2cwUA.jpg)

Git 中，使用 HEAD 表示目前的版本，

```cmd
git reset --hard HEAD
```

![alt tag](http://i.imgur.com/pkFO8pk.jpg)

如果現在要把目前版本退回到上一個版本，就可以使用 git reset 指令：

上一個版本就是HEAD~1，

```cmd
git reset --hard HEAD~1
```

![alt tag](http://i.imgur.com/ZThoaUT.jpg)

上上一個版本就是HEAD~2，

如果要指定回到某個特定版本：

![alt tag](http://i.imgur.com/KrCOC71.jpg)

```cmd
git reset --hard ad41df36b7
```

![alt tag](http://i.imgur.com/6RVutiK.jpg)

版本號 ( ad41df36b7 ) 沒必要全部都寫，寫前幾位就可以了，Git 會自動去找。

當你退回到某個版本，突然隔天後悔了，想恢復到之前的新版本該怎麼做呢?

找不到新版本的 commit id 該怎麼辦呢?

這時候就可以使用一個指令

```cmd
git reflog
```

![alt tag](http://i.imgur.com/MaRlZZr.jpg)

接著看你要回到哪個版本，再使用 git reset 即可。

```cmd
git reset --hard 642e7af
```

有時候想消除( 覆蓋 )已經 push 出去的 commit，這時候我們可以使用

```cmd
git push --force
```

或是更簡短的寫法

```cmd
git push -f
```

可以強制 push。先回到某個版本，然後再強制 push。

***注意！在多人專案共同開發時，盡量不要用 --force 這種方法，因為有時候會害到別人，建議可以使用 revert 。***

## checkout

git checkout -- file 可以丟棄工作區的修改：

```cmd
git checkout  -- hello.py
```

命令 git checkout -- hello.py 意思就是，把 hello.py 文件在工作區的修改全部撤銷 ( 丟棄 ) ，

讓這個檔案回到最近一次 git commit 或 git add 時的狀態。

![alt tag](http://i.imgur.com/SrCo4kH.jpg)

當然也可以用 git reset 指令直接回到某個 commit。

```cmd
git reset --hard xxxxxx
```

```cmd
git reset --hard 201f40604ec3b6fa8
```

## 刪除

有兩種況狀，一種是確定要從版本庫中刪除該檔案，那就用命令 git rm 刪掉，並且 git commit：

```cmd
rm hello.py
git rm hello.py
git commit -m "remove hello.py"
```

![alt tag](http://i.imgur.com/sLMTDX7.jpg)

另一種況狀是刪錯了，使用 git checkout 可以輕鬆還原檔案:

```cmd
rm hello.py
git checkout -- hello.py
```

![alt tag](http://i.imgur.com/5X2NcfS.jpg)

## 新建與 合併 ( merge ) 分支 branch

再說明 分支 branch 之前，先給大家一個觀念。

通常再開發的時候，大家都是從 **master** 做一個 分支 branch 出去，最後再 **merge** 回 master，

為什麼要這麼做呢 ?  因為要確保大家都是使用最新的 **master**

使用 git branch 指令查看目前的分支：

```cmd
git branch
```

![alt tag](http://i.imgur.com/SVblXD2.jpg)

首先創建一個分支，bug1 分支 ( 名稱可以隨便取 )，然後切換到 bug1 分支：

```cmd
git branch bug1
git checkout bug1
```

git branch bug1 為創造一個名稱為 bug1 的分支，

git checkout bug1 為切換到一個名稱為 bug1 的分支底下。

![alt tag](http://i.imgur.com/JtGBHk4.jpg)

以上兩行指令，相當於下列一行指令

```cmd
git checkout -b bug1
```

我們在 bug1 分支上進行任何修改操作，

然後再把工作成果 ( 補充一下，修改任何內容後請記得使用 git add 指令和 git commit 指令 ) 合併到 master 分支上：

```cmd
git checkout master
git merge bug1
```

![alt tag](http://i.imgur.com/pF4xDUE.jpg)

git checkout master 為切換到一個名稱為 master 的分支底下。

git merge bug1 指令用於合併 ( bug1分支 ) 指定分支到目前分支 ( master ) 底下。

如果非常順利， git merge 的訊息裡會出現 Fast-forward，合併速度非常快。

當然不是每次合併都能很順利的出現 Fast-forward，很多時候會出現衝突 CONFLICT 。

如果順利合併 ( merge ) 完成後，就可以刪除 bug1 分支：

```cmd
git branch -d dev
```

![alt tag](http://i.imgur.com/LmKKWxR.jpg)

如果要丟掉一個沒有被合併過的分支，可以使用 git branch -D 分支名稱  強行刪除。

```cmd
git branch -D dev
```

## 新建分支 branch 並 push

相信大家有時候在 github 上面都會看到，如下圖，很多分支

![alt tag](http://i.imgur.com/wrIdlzS.jpg)

那我們要如何建立分支呢? 首先，我們先看下面這張圖

![alt tag](http://i.imgur.com/3U092a1.jpg)

有一個 v1 的分支，並且我在分支上增加一個 g.py 並且 commit。

接下來要 **第一次** git push 的時候， 你會發現有錯誤提示

請使用以下指令才是正確的

```cmd
git push --set-upstream origin v1
```

![alt tag](http://i.imgur.com/1fuS2VY.jpg)

接下來你可以到網頁上看 ( 這裡用 bitbucket 當作範例 ) ，你會發現有分支 v1 了

![alt tag](http://i.imgur.com/lOtzsk8.jpg)

如果是第一次使用 git clone ，你會發現你只有 master 分支 ，

這時候我們先查看遠端還有什麼分支，

```cmd
git branch -r
```

假設遠端有一個名稱為 develop 的分支，

我們只要 checkout 到該分支底下就可以了

```cmd
git checkout develop
```

## git pull

通常在開始工作或要 push 之前，會先從遠端抓取分支，

```cmd
git pull
```

如果有衝突，要先解衝突。

## git fetch

可以先簡單想成 **git pull = git fetch + git merge**

我們先來看下面這張圖，  **git fetch + git merge**

![alt tag](http://i.imgur.com/COuWByw.png)

再看這張圖  **git pull**

![alt tag](http://i.imgur.com/8FGuA75.png)

這樣是不是清楚多了!!!

## git rebase

什麼是 rebase 呢 ? git rebase 就是避免多餘 ( 沒有意義 ) 的 merge !!! 先看看下面兩張圖

補充 :

ck = checkout

br = branch

st = status

cm = commit

可以自行設定。

圖一

![alt tag](http://i.imgur.com/mWY0f2J.png)

圖二

![alt tag](http://i.imgur.com/QVZc5P5.png)

圖一 和 圖二 你喜歡看哪種圖 ?  答案很明顯，是 圖一 !!

**rebase** 的目的主要就是盡量讓圖都像 圖一

用講的大家一定霧煞煞，所以我直接實戰給大家看。

先示範 **沒有使用 rebase** 的範例

目前分支

![alt tag](http://i.imgur.com/E0ahfnD.png)

![alt tag](http://i.imgur.com/Lb4dB0V.png)

以上說明 : 先建立 v1 branch，接著 add 後再 commit。

假設現在又有人 push 了，以下模擬 pull ，自己加上一個 commit

![alt tag](http://i.imgur.com/hFKX4yJ.png)

以上說明 : 自己在 master 分支上加 t2.txt ， 並且commit ( 模擬 pull )

接下來，切換到 master 分支下和 v1 branch 分支 合併，並且 push

![alt tag](http://i.imgur.com/0sCH2Q1.png)

你會發現，顯示出來的圖並不漂亮，如下圖

![alt tag](http://i.imgur.com/zbIPdyb.png)

示範 **使用 rebase** 的範例

前面的部份基本上一樣

![alt tag](http://i.imgur.com/E0ahfnD.png)

![alt tag](http://i.imgur.com/Lb4dB0V.png)

以上說明 : 先建立 v1 branch，接著 add 後再 commit。

假設現在又有人 push 了，以下模擬 pull ，自己加上一個 commit

![alt tag](http://i.imgur.com/hFKX4yJ.png)

以上說明 : 自己在 master 分支上加 t2.txt ， 並且 commit ( 模擬 pull )

***差異的部份***

![alt tag](http://i.imgur.com/45ZXGiK.png)

以上說明 : 先切換到 v1 分支，然後使用以下指令

```cmd
git rebase master
```

![alt tag](http://i.imgur.com/Lpd9Kjr.png)

以上說明 : 再切回 master 分支，並且使用 merge 合併 v1 分支，最後在 push

你看~  是不是變的整齊又漂亮多了呢?

![alt tag](http://i.imgur.com/1jBI7pw.png)

git rebase  就是將 master 的最新 commit 接回來，再補上自己分支的 commit。

以上就是 git rebase  的介紹。

## git revert

假設我 commit history 為 A1 -> A2 -> A3 -> A4 -> A5 -> A6

我現在想要回 A4 這個 commit , 這時候我就可以使用  git revert ！！

先 revert A6

```cmd
git revert A6
```

再 revert A5

```cmd
git revert A5
```

假如你再看現在的 commit history , 他會長的像這樣

A1 -> A2 -> A3 -> A4 -> A5 -> A6 -> A6_revert -> A5_revert

這時候，其實你的 commit 就是在 A4 這個位置 。

使用 git revert 的好處，就是可以保留 commit history , 萬一你又後悔了，

也可以在 revert 回去。

## 解決衝突

在進行合併的時候，有時候會顯示出 **衝突conflicts** ，這時候就必須手動解決衝突後再送出。

通常我目前最容易遇到衝突 conflicts ，就是使用 pull 這個指令的時候

![alt tag](http://i.imgur.com/Eph0Vw1.jpg)

仔細看這張圖，如果使用**pull**這個指令，會幫你 **自動 merge** ( 如圖裡的 Auto-merging Hello.py )，

然後接著看 CONFLICT ( content ) : Merge conflict in Hello.py ，又說 Automatic merge failed，

就是告訴你， Hello.py 這個檔案有衝突，然後你必須手動下去解決衝突。

git status 可以告訴我們衝突的文件。

![alt tag](http://i.imgur.com/vlVcXn8.jpg)

打開衝突文件我們會看到 Git 用 <<<<<<<，=======，>>>>>>> 標記出不同分支的內容，我們修改完畢後再提交：

![alt tag](http://i.imgur.com/rlPOaxn.jpg)

通常我們會手動下去修改衝突 conflicts，然後再加個 commit

```cmd
git add Hello.py
git commit -m "conflict fixed"
```

### 假設今天我們想要放棄這個 merge 我們該怎麼做呢 ？

```cmd
git merge --abort
```

或

```cmd
git reset --hard HEAD
```

可以取消這次的 merge 回到 merge 前。

## git stash 指令

很多時候，我們正在開發一個新功能又或是 debug，然後突然有一個功能需要緊急修正，

但你又不想 commit 現在的狀況，因為根本沒意義，事情只做了一半，這時候 **stash**

這個實用的指令就派上用場了。

舉個例子，假設我們改了 A.py 和 B.py 這兩個檔案

![alt tag](http://i.imgur.com/7xX0T1T.jpg)

然後，現在突然有一個bug必須馬上 ( 立刻 ) 處理，但是，啊我手上的事情還沒做完阿~~~~
這時候，可以利用以下指令

```cmd
git stash
```

![alt tag](http://i.imgur.com/cYCH8mV.jpg)

假如你想要更清楚自己這次的 stash 原因是什麼，或是這是正在開發什麼功能
可以使用以下指令

```cmd
git stash save -u "我是註解"
```

```cmd
git stash save -u "feature"
```

![alt tag](http://i.imgur.com/nGS11Px.jpg)

接下來你可以使用 status 指令，你會發現變乾淨了

![alt tag](http://i.imgur.com/Xf53GfM.jpg)

並且可以使用下列的指令來觀看 stash 裡面的東西

```cmd
git stash list
```

![alt tag](http://i.imgur.com/jQPiYiX.jpg)

然後你很努力地解決這個 bug，commit 完之後，
可以再使用下列的指令把 stash 取回來，這指令取回後也會刪除 stash

```cmd
git stash pop
```

假設今天你有很多的 stash，你可以指定，如下

```cmd
git stash pop stash@{0}
```

![alt tag](http://i.imgur.com/zVF7no2.jpg)

你會發現剛剛的東西回來了~

如果你希望使用 stash 取回之後，不希望刪除 stash ，可以使用下列的指令

```cmd
git stash apply
```

如下圖，你可以發現取回後， stash 並沒有被刪除

![alt tag](http://i.imgur.com/w3Ip3iW.jpg)

如果你只是想要刪除暫存，可以使用下列的指令

```cmd
git stash clear
```

從下圖可以發現，stash 裡面的東西被我們刪除了

![alt tag](http://i.imgur.com/PvzufbQ.jpg)

如果你想丟棄指定的 stash，可以使用

```cmd
git stash drop stash@{0}
```

## git 其他設定

我們已經設定了 user.name 以及 user.email ，但 Git 上其實還有很多可設定的東西

有時候，我們必須把某些檔案 ( 文件夾 ) 放到 Git 工作目錄中，但又不能提交它們，

像是密碼設定或是編譯器 IDE 產生出來的東西之類的，

每次 git status 都會看到紅紅的 Untracked files ，通常會覺得有點煩......

這問題 Git 也幫我們想過，只要在 Git 工作區的根目錄下新建一個特殊的 **.gitignore** 文件 ，

然後把要忽略的文件 ( 檔案 ) 名稱輸入進去， Git 就會自動忽略這些文件。

當然不需要自己從頭寫 .gitignore 文件， GitHub 已經幫我們準備了一些文件 [gitignore](https://github.com/github/gitignore)

**.gitignore** 檔案直接放在目錄底下即可

![alt tag](http://i.imgur.com/8rHPsII.jpg)

### .gitignore 檔案格式範例

![alt tag](http://i.imgur.com/W3cxk9r.jpg)

有時候常常手殘 key 錯指令或是記不起來

如果我們打 git st 就表示 git status 那該有多棒!!!

所以我們可以自己設定，讓 Git 以後打 **git st = git status**
如下圖，原本不能使用 git st ，設定完之後就可以使用了。

```cmd
git config --global alias.st status
```

![alt tag](http://i.imgur.com/4NNasgB.jpg)

```cmd
git config --global alias.br branch
```

![alt tag](http://i.imgur.com/NIc71AO.jpg)

```cmd
git config --global alias.ck checkout
```

```cmd
git config --global alias.cm commit
```

可能有人會問，那這個設定檔文件在哪裡呢?

通常會在你的使用者底下，例如我這台電腦使用者為 HJ，設定檔文件就會在 **C:\Users\HJ** 底下，

他是一個  **隱藏文件.gitconfig** ，打開他的話格式如下。

![alt tag](http://i.imgur.com/iXjIqv9.jpg)

## 使用 Git 一次 Push 到多個不同的遠端 ( remote )

假如有一天 github 掛了，這樣是不是就不能 work 了，你可能會說本地端還有 ?

但......多備份絕對是好事 !!  再這裡介紹如何一次 Push 到多個不同的遠端 ( remote )

這裡用 [Bitbucket](https://bitbucket.org/product) 當作範例

先使用下方指令查看

```cmd
git remote -v
```

![alt tag](http://i.imgur.com/Qb5VHoP.png)

接著我們使用下列指令新增一個 origin 的遠端

```cmd
git remote set-url --add origin <url>
```

```cmd
git remote set-url --add origin git@github.com:twtrubiks/test2.git
```

![alt tag](http://i.imgur.com/FKzexVE.png)

我們再用 git remote -v 查看一次，你會發現多了剛剛新增的遠端 ( remote )

![alt tag](http://i.imgur.com/p1q7C4b.png)

最後我們再 push

![alt tag](http://i.imgur.com/6VKh8Bz.png)

仔細看，是不是一次 push 到多個不同的遠端 ( remote )，非常方便!!

***GitHub***

![alt tag](http://i.imgur.com/JljPJHJ.png)

***Bitbucket***

![alt tag](http://i.imgur.com/rkYHNl4.png)

P.S 設定檔在資料夾底下的隱藏檔 ".git" 底下，裡面有一個 config

![alt tag](http://i.imgur.com/41xb8eu.png)
