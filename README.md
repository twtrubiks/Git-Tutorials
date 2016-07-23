# Git-Tutorials 基本使用教學:memo:
因為小弟覺得這東西蠻有趣的，所以就簡單寫個教學文，順便記錄一下:memo:

如果教學有誤再請糾正，很多也是參考網路上的教學文，在這裡簡單整理一下，希望能幫助想學的人:smile:

基本使用指令以及安裝可參考小弟之前拍的影片[github基本教學 - 從無到有](https://www.youtube.com/watch?v=py3n6gF5Y00)

影片教學包含如何產生<b>SSH key</b>

如果步驟正確且沒出錯誤，可以路徑下找到<b>.ssh資料夾</b>，裡面有<b>id_rsa</b>以及<b>id_rsa.pub/<b>兩個檔案，

這兩個就是SSH Key，<b>id_rsa是私鑰</b>，不能洩露出去，<b>id_rsa.pub是公鑰</b>，可以很放心的告訴任何人。

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

Git設定資料查看，可執行以下指令(文章末會有較詳細的教學)：
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

如圖(下載成功)，在你的下載路徑下就會多出一個資料夾
![alt tag](http://i.imgur.com/iIkTlqf.jpg)

## git status 指令
```
git status
```

可以讓我們觀看目前的repository(repo 容器)。

![alt tag](http://i.imgur.com/5Gt98Vh.jpg)

意思是目前你的工作區是乾淨的。


## 工作區與暫存區(Stage)

git add 意思是把要送出的文件放到暫存區(Stage)，

然後執行

git commit 就可以把暫存區(Stage)裡所有修改的內容送到目前的分支上。

一旦送出(git commit)後，如果你又沒有對工作區做任何修改，那麼工作區就是"乾淨"的。

git commit -m "xxxxx"指令，-m 後面輸入的內容是本次修改(送出)的說明，

盡量輸入一眼就可以看出這次送出修改了什麼的內容
(方便以後回去觀看能快速了解此次commit修改了什麼)。

以下demo為在一個資料夾內新增一個 Hello.py 檔案

然後使用git status 觀看目前的repository(repo 容器)，你會看到Hello.py未被追蹤，如下圖

![alt tag](http://i.imgur.com/dvj1DQh.jpg)

可以使用如下指令
```
git add Hello.py
```

接著再使用</br>
git commit -m "文字"
```
git commit -m "add Hello.py"
```
再使用git status，你會發現工作區變乾淨了。如下圖<br>

![alt tag](http://i.imgur.com/6VrieNb.jpg)


## git push 指令
```
git push 
```
將程式push到github(or bitbucket 之類 )上,如下圖<br>

![alt tag](http://i.imgur.com/d61Pau6.jpg)

## 版本控制 - 歷史記錄
```
git log
```
按<b>小寫q<b>可退出<br>
![alt tag](http://i.imgur.com/j11afCP.jpg)

如果覺得版面太雜，可以使用下列指令
```
git log --pretty=oneline
```
按按<b>小寫q<b>可退出<br>
![alt tag](http://i.imgur.com/jz2cwUA.jpg)


Git中，使用HEAD表示目前的版本， 
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

如果要指定回到某個特定版本：

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

有時候想消除(覆蓋)已經push出去的commit，這時候我們可以使用
```
git push --force 
```
可以強制push，先回到某個版本，然後再強制push。

## checkout

git checkout -- file 可以丟棄工作區的修改：
```
git checkout  -- hello.py
```
命令git checkout -- hello.py意思就是，

![alt tag](http://i.imgur.com/Moua6Ho.jpg)

把hello.py文件在工作區的修改全部撤銷(丟棄)，讓這個檔案回到最近一次git commit或git add時的狀態。

當然也可以用git reset指令直接回到某個commit。
git reset --hard xxxxxx
```
git reset --hard 201f40604ec3b6fa8
```

## 刪除

現在你有兩個選擇，一是確實要從版本庫中刪除該文件，那就用命令git rm刪掉，並且git commit：

git rm hello.py
git commit -m "remove hello.py"

![alt tag](http://i.imgur.com/zhY0I9t.jpg)

另一種情況是刪錯了，因為版本庫裡還有呢，所以可以很輕鬆地把誤刪的文件恢復到最新版本：

git rm hello.py
git checkout -- hello.py

![alt tag](http://i.imgur.com/Moua6Ho.jpg)
## 新建與合併分支 branch

使用git branch指令查看目前的分支：
```
git branch
```
![alt tag](http://i.imgur.com/SVblXD2.jpg)


首先創建一個分支，bug1分支(名稱可以隨便取)，然後切換到bug1分支：
```
git branch bug1
git checkout bug1
```
git branch bug1 為創造一個名稱為bug1的分支，<br>
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

git checkout master為切換到一個名稱為master的分支底下。<br>
git merge bug1 指令用於合併(bug1分支)指定分支到目前分支(master)底下。

如果非常順利，git merge的訊息裡會出現Fast-forward，合併速度非常快

當然不是每次合併都能很順利的出現Fast-forward，很多時候會出現衝突CONFLICT

如果順利合併完成後，就可以刪除bug1分支：
```
git branch -d dev
```
![alt tag](http://i.imgur.com/LmKKWxR.jpg)<br>
如果要丟掉一個沒有被合併過的分支，可以使用 git branch -D 分支名稱  強行刪除。
```
git branch -D dev
```
從遠程抓取分支，使用git pull，如果有衝突，要先處理衝突


## 解決衝突

在進行合併的時候，有時候會顯示出 <b>衝突conflicts<b>，這時候就必須手動解決衝突後再送出。

通常我目前最容易遇到衝突conflicts，就是使用pull這個指令的時候

![alt tag](http://i.imgur.com/Eph0Vw1.jpg)<br>
仔細看這張圖，如果使用<b>pull<b>這個指令，會幫你<b>自動merge<b> (如圖裡的Auto-merging Hello.py)，

然後接著看 CONFLICT (content): Merge conflict in Hello.py ，又說 Automatic merge failed，

就是告訴你，Hello.py這個檔案有衝突，然後你必須手動下去解決衝突。


git status可以告訴我們衝突的文件。

![alt tag](http://i.imgur.com/vlVcXn8.jpg)

打開衝突文件我們會看到Git用<<<<<<<，=======，>>>>>>>標記出不同分支的內容，我們修改完畢後再提交：

![alt tag](http://i.imgur.com/rlPOaxn.jpg)

通常我們會手動下去修改衝突conflicts，然後再加個 commit
```
git add Hello.py
git commit -m "conflict fixed"
```

## git其他設定
我們已經設定了user.name以及user.email，但Git上其實還有很多可設定的東西

有時候，我們必須把某些檔案(文件夾)放到Git工作目錄中，但又不能提交它們，像是密碼設定或是編譯器IDE產生出來的東西之類的，<br>
每次git status都會看到紅紅的Untracked files，通常會覺得有點煩......

這問題Git也幫我們想過，只要在Git工作區的根目錄下新建一個特殊的<b>.gitignore</b>文件，然後把要忽略的文件(檔案)名稱輸入進去，Git就會自動忽略這些文件。

當然不需要自己從頭寫.gitignore文件，GitHub已經幫我們準備了一些文件[gitignore](https://github.com/github/gitignore)
<br><br>
<b>.gitignore<b>檔案直接放在目錄底下即可
<br>
![alt tag](http://i.imgur.com/8rHPsII.jpg)
<br>
<b>.gitignore檔案格式範例</b>
<br>
![alt tag](http://i.imgur.com/W3cxk9r.jpg)
<br>

有時候常常手殘key錯指令或是記不起來

如果我們打git st就表示git status那該有多棒!!!

所以我們可以自己設定，讓Git以後打 <b>git st = git status</b>
如下圖，原本不能使用git st，設定完之後就可以使用了。
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
通常會在你的使用者底下，例如我這台電腦使用者為HJ，設定檔文件就會在 <b>C:\Users\HJ</b> 底下，<br>
他是一個  <b>隱藏文件.gitconfig</b> ，打開他的話格式如下。
<br>
![alt tag](http://i.imgur.com/iXjIqv9.jpg)


