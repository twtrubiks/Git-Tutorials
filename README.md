# Git-Tutorials 基本使用教學
Git-Tutorials  GIT基本使用教學
因為小弟覺得這東西蠻有趣的，所以就簡單寫個教學文，如果教學有誤再請糾正，很多也是參考網路上的教學文，在這裡整理一下，希望能幫助想學的人:memo:

基本使用指令以及安裝可參考小弟之前拍的影片[github基本教學 - 從無到有](https://www.youtube.com/watch?v=py3n6gF5Y00)

影片教學包含如何產生SSH key

如果步驟正確且沒出錯誤，可以路徑下找到.ssh資料夾，裡面有id_rsa以及id_rsa.pub兩個檔案，

這兩個就是SSH Key的秘鑰對，id_rsa是私鑰，不能洩露出去，id_rsa.pub是公鑰，可以放心的告訴任何人。

安裝完Git之後，要做的第一件事情就是去設定自己的名字和信箱
```
git config --global user.name "twtrubiks"
git config --global user.email "twtrubiks@gmail.com"
```

可以輸入以下來確認是否輸入成功
```
git config --global user.name
git config --global user.email
```
![alt tag](http://i.imgur.com/5mpS7Ij.jpg)

Git設定資料，可執行以下指令：
```
git config --list
```

## git clone 指令

複製如圖位置網址 (不要複製我的哦~ 複製你自己的)
![alt tag](http://i.imgur.com/EJ5JNjt.jpg)

git clone (複製的網址)
```
git clone git@github.com:twtrubiks/test.git
```

第一次會出現SSH警告，選YES即可。

如圖(下載成功)
![alt tag](http://i.imgur.com/iIkTlqf.jpg)

## git status 指令
```
git status
```

可以讓我們觀看目前的repository(repo 容器)。

![alt tag](http://i.imgur.com/5Gt98Vh.jpg)

意思為目前你的工作區是乾淨的。


## 工作區與暫存區

git add 意思是把要送出的文件放到暫存區(Stage)，

然後執行

git commit 就可以把暫存區(Stage)裡所有修改的內容送到目前的分支上。

一旦送出後，如果你又沒有對工作區做任何修改，那麼工作區就是"乾淨"的。

commit指令

git commit指令，-m 後面輸入的內容是本次送出的說明，盡量輸入一眼就可以看出這次送出修改了什麼的內容
(方便以後回去觀看能快速了解此次commit修改了什麼)。

以下demo為在一個資料夾內新增一個 Hello.py 檔案

然後使用git status 觀看目前的repository(repo 容器)，你會看Hello.py未被追蹤，到如下圖

![alt tag](http://i.imgur.com/dvj1DQh.jpg)

可以使用如下指令
```
git add Hello.py
```

接著再使用
git commit -m "文字"
```
git commit -m "add Hello.py"
```
再使用git status，你會發現工作區變乾淨了。

如下圖<br>
![alt tag](http://i.imgur.com/6VrieNb.jpg)


## git push 指令
```
git push 
```
將程式push到github(or bitbucket 之類 )上

如圖<br>
![alt tag](http://i.imgur.com/d61Pau6.jpg)

## 版本控制 - 歷史記錄
```
git log
```
按小寫q可退出<br>
![alt tag](http://i.imgur.com/j11afCP.jpg)

如果覺得版面太雜，可以使用下列指令
```
git log --pretty=oneline
```
按小寫q可退出<br>
![alt tag](http://i.imgur.com/jz2cwUA.jpg)


Git中，可以使用HEAD表示目前的版本， 
```
git reset --hard HEAD
```
![alt tag](http://i.imgur.com/pkFO8pk.jpg)

如果現在要把目前版本退回到上一個版本，就可以使用git reset指令：

上一個版本就是HEAD~1，
```
git reset --hard HEAD~1
```
![alt tag](http://i.imgur.com/ZThoaUT.jpg)
<br>
上上一個版本就是HEAD~2，

指定回到某個版本：

![alt tag](http://i.imgur.com/KrCOC71.jpg)
```
git reset --hard ad41df36b7
```
![alt tag](http://i.imgur.com/6RVutiK.jpg)<br>
版本號(ad41df36b7)沒必要全部都寫，寫前幾位就可以了，Git會自動去找。


當你退回到某個版本，突然隔天後悔了，想恢復到之前的新版本該怎麼做呢?

找不到新版本的commit id該怎麼辦呢?

這時候就可以使用一個指令
```
git reflog
```
![alt tag](http://i.imgur.com/MaRlZZr.jpg)

git reset --hard 642e7af

有時候想消除已經push出去的commit，這時候我們可以使用
```
git push --force 
```
可以強制push


## checkout

git checkout -- file可以丟棄工作區的修改：
```
git checkout  -- hello.py
```
命令git checkout -- hello.py意思就是，

![alt tag]http://i.imgur.com/Moua6Ho.jpg)

把hello.py文件在工作區的修改全部撤銷，即讓這個文件回到最近一次git commit或git add時的狀態。

當然也可以用git reset命令
```
git reset --hard 201f40604ec3b6fa8
```

## 刪除

現在你有兩個選擇，一是確實要從版本庫中刪除該文件，那就用命令git rm刪掉，並且git commit：

git rm hello.py
git commit -m "remove hello.py"

![alt tag](http://i.imgur.com/81To98u.jpg)

另一種情況是刪錯了，因為版本庫裡還有呢，所以可以很輕鬆地把誤刪的文件恢復到最新版本：

git rm hello.py
git checkout -- hello.py

![alt tag](http://i.imgur.com/Moua6Ho.jpg)
## 創建與合併分支 branch

可以使用git branch指令查看目前的分支：
```
git branch
```
![alt tag](http://i.imgur.com/SVblXD2.jpg)


首先創建一個分支，bug1分支(名稱可以隨便取)，然後切換到bug1分支：
```
git branch bug1
git checkout bug1
```
git branch bug1 為創造一個名稱為bug1的分支，
git checkout bug1為切換到一個名稱為bug1的分支底下。
![alt tag](http://i.imgur.com/JtGBHk4.jpg)

以上兩行指令，相當於下列一行指令
```
git checkout -b bug1
```

我們在bug1分支上進行任何修改操作，然後再把工作成果(補充一下，修改任何內容後請記得使用git add指令和git commit指令)合併到master分支上：
```
git checkout master
git merge bug1
```

![alt tag](http://i.imgur.com/pF4xDUE.jpg)

git checkout master為切換到一個名稱為master的分支底下。
git merge bug1 指令用於合併(bug1分支)指定分支到目前分支(master)底下。

如果非常順利，git merge的訊息裡會出現Fast-forward，合併速度非常快

當然不是每次合併都能很順利的出現Fast-forward，很多時候會出現衝突CONFLICT

如果順利合併完成後，就可以刪除bug1分支：
```
git branch -d dev
```
![alt tag](http://i.imgur.com/LmKKWxR.jpg)<br>
如果要丟棄一個沒有被合併過的分支，可以通過git branch -D <branch>強行刪除。

從遠程抓取分支，使用git pull，如果有衝突，要先處理衝突


## 解決衝突

在進行合併的時候，有時候會顯示出 衝突conflicts，這時候就必須手動解決衝突後再送出。

通常我目前最容易遇到衝突conflicts，就是使用pull這個指令的時候

![alt tag](http://i.imgur.com/Eph0Vw1.jpg)<br>
指細看這張圖，如果使用pull這個指令，會幫你自動merge (如圖裡的Auto-merging Hello.py)，

然後接著看 CONFLICT (content): Merge conflict in Hello.py ，又說 Automatic merge failed;


git status可以告訴我們衝突的文件。

![alt tag](http://i.imgur.com/vlVcXn8.jpg)

打開衝突文件我們會看到Git用<<<<<<<，=======，>>>>>>>標記出不同分支的內容，我們修改完畢後再提交：

![alt tag](http://i.imgur.com/rlPOaxn.jpg)

通常我們會手動下去修改衝突conflicts，然後再加個 commit
git add Hello.py
git commit -m "conflict fixed"


## git其他設定
我們已經設定user.name以及user.email，但Git上其實還有很多可設定的東西


有些時候，你必須把某些文件放到Git工作目錄中，但又不能提交它們，比如保存了數據庫密碼的配置文件啦，等等，每次git status都會顯示Untracked files…，有強迫症的童鞋心里肯定不爽。

好在Git考慮到了大家的感受，這個問題解決起來也很簡單，在Git工作區的根目錄下創建一個特殊的.gitignore文件，然後把要忽略的文件名 ​​填進去，Git就會自動忽略這些文件。

不需要從頭寫.gitignore文件，GitHub已經為我們準備了各種配置文件，只需要組合一下就可以使用了。
<br>
所有配置文件可以直接在線瀏覽：https://github.com/github/gitignore
<br>
.gitignore放在目錄底下
<br>
![alt tag](http://i.imgur.com/8rHPsII.jpg)
<br>
.gitignore文件格式
<br>
![alt tag](http://i.imgur.com/W3cxk9r.jpg)
<br>

有時候常常key錯指令感到很煩 ? 像是git status常常打錯或記不起來

如果打git st就表示git status那該有多棒!!!

所以我們可以自己設定，讓Git以後打 git st = git status
```
git config --global alias.st status
```
![alt tag](http://i.imgur.com/4NNasgB.jpg)
```
git config --global alias.br branch
```
![alt tag](http://i.imgur.com/NIc71AO.jpg)
```
git config --global alias.ck checkout
```
```
git config --global alias.cm commit
```
<br>
可能有人會問，那這個設定檔文件在哪裡呢?
<br>
通常會在你的使用者底下，例如我這台電腦使用者為HJ，設定檔文件就會在 C:\Users\HJ 底下，
他是一個  隱藏文件.gitconfig ，打開他格式如下。
<br>
![alt tag](http://i.imgur.com/iXjIqv9.jpg)


在撤銷修改一節中，我們知道，命令git reset HEAD file可以把暫存區的修改撤銷掉（unstage），重新放回工作區。

既然是一個unstage操作，就可以配置一個unstage別名：

git config --global alias.unstage 'reset HEAD'
配置一個git last，讓其顯示最後一次提交信息：















======================================以下待整理===============================================

![alt tag]()
![alt tag]()
![alt tag]()
Bug分支

軟件開發中，bug就像家常便飯一樣。有了bug就需要修復，在Git中，由於分支是如此的強大，所以，每個bug都可以通過一個新的臨時分支來修復，修復後，合併分支，然後將臨時分支刪除。

當你接到一個修復一個代號101的bug的任務時，很自然地，你想創建一個分支issue-101來修復它，但是，等等，當前正在dev上進行的工作還沒有提交。

並不是你不想提交，而是工作只進行到一半，還沒法提交，預計完成還需1天時間。但是，必須在兩個小時內修復該bug，怎麼辦？

幸好，Git還提供了一個stash功能，可以把當前工作現場“儲藏”起來，等以後恢復現場後繼續工作：

git stash
現在，用git status查看工作區，就是乾淨的（除非有沒有被Git管理的文件），因此可以放心地創建分支來修復bug。

首先確定要在哪個分支上修復bug，假定需要在master分支上修復，就從master創建臨時分支：

git checkout master
git checkout -b issue-101
現在修復bug，然後提交：

git add readme.md
git commit -m "fix bug 101"
修復完成後，切換到master分支，並完成合併，最後刪除issue-101分支：

git checkout master
git merge --no-ff -m "merged bug fix 101" issue-101
太棒了，原計劃兩個小時的bug修復只花了5分鐘！現在，是時候接著回到dev分支幹活了！

git checkout dev
git status
工作區是乾淨的，剛才的工作現場存到哪去了？用git stash list命令看看：

git stash list
工作現場還在，Git把stash內容存在某個地方了，但是需要恢復一下，有兩個辦法：

一是用git stash apply恢復，但是恢復後，stash內容並不刪除，你需要用git stash drop來刪除；

另一種方式是用git stash pop，恢復的同時把stash內容也刪了：

git stash pop
再用git stash list查看，就看不到任何stash內容了。

你可以多次stash，恢復的時候，先用git stash list查看，然後恢復指定的stash，用命令

git stash apply stash@{0}
標籤管理

發布一個版本時，我們通常先在版本庫中打一個標籤，這樣，就唯一確定了打標籤時刻的版本。將來無論什麼時候，取某個標籤的版本，就是把那個打標籤的時刻的歷史版本取出來。所以，標籤也是版本庫的一個快照。

命令git tag <tagname>用於新建一個標籤，默認為HEAD，也可以指定一個commit id。

git tag -a <tagname> -m "blablabla..."可以指定標籤信息。

還可以通過-s用私鑰簽名一個標籤：

git tag -s v0.5 -m "signed version 0.2 released" fec145a
git tag可以查看所有標籤。

用命令git show <tagname>可以查看某個標籤的詳細信息。

如果標籤打錯了，也可以刪除：

git tag -d v0.1
因為創建的標籤都只存儲在本地，不會自動推送到遠程。所以，打錯的標籤可以在本地安全刪除。

如果要推送某個標籤到遠程，使用命令git push origin <tagname>：

git push origin v1.0
或者，一次性推送全部尚未推送到遠程的本地標籤：

git push origin --tags
如果標籤已經推送到遠程，要刪除遠程標籤就麻煩一點，先從本地刪除：

git tag -d v0.9
然後，從遠程刪除。刪除命令也是push，但是格式如下：

git push origin :refs/tags/v0.9
忽略特殊文件

