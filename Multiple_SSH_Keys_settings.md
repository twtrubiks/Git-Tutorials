# Multiple SSH Keys settings for different github account

如果你對這個真的很陌生，建議看影片:smile:

* [Youtube Tutorial - Multiple SSH Keys settings for different github account](https://youtu.be/gDxG-4tF7B8)

## 前言

有時候我們可能會遇到這種情境，就是同一台電腦上同時需要有多個 github 帳號，為什麼呢?

當你工作的電腦和你自己的 side project 開發都在同一台電腦的時候，你就需要這篇文章的幫忙

了 :kissing_smiling_eyes:

相信我，你不會希望用公司的帳號推 commit 到自己的 side project 上:sweat_smile:

## 教學

第一步，先產生 ssh key，如果你不知道怎麼產生，

可參考 [Generating a new SSH key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/) 或是 [github基本教學 - 從無到有](https://www.youtube.com/watch?v=py3n6gF5Y00)，

打開你的 Git Bash，

```cmd
ssh-keygen -t rsa -b 4096 -C "blue555236sa56@gmail.com"
```

( 請將信箱換成自己的 )

這裡的重點是記得自行輸入新的 rsa 名稱，像是下圖的 `/c/Users/twtrubiks/.ssh/id_rsa_rubik` 這樣，

這樣才不會覆蓋舊有的 rsa，

![alt tag](https://i.imgur.com/2Msr51U.png)

接下來，你的 `.ssh` 路徑底下會多出你剛剛建立的檔案

![alt tag](https://i.imgur.com/B4g9FQO.png)

再把你的  `id_rsa_rubik.pub` key 貼到你的 gihub 上，

![alt tag](https://i.imgur.com/tfQzFcJ.png)

通常你新增成功的時候，信箱會收到一封信。

再輸入下方指令

```cmd
ssh-agent -s
```

上面這個指令一定要執行，如果跳過這個步驟，就會出現以下錯誤，

Could not open a connection to your authentication agent.

所以請記得一定要執行。

在 `.ssh` 目錄底下建立一個名稱為 `config` 的檔案 ( 檔名就是 `config`，副檔名不用填 )，

![alt tag](https://i.imgur.com/SJBxro6.png)

下方是一個範例，

```config
# github - twtrubiks
    Host github.com
    HostName github.com
    IdentityFile ~/.ssh/id_rsa
    IdentitiesOnly yes
    User twtrubiks

# github - blue-rubiks
    Host blue.github.com
    HostName github.com
    IdentityFile ~/.ssh/id_rsa_rubik
    IdentitiesOnly yes
    User blue-rubiks
```

可用以下指令測試，如果顯示出自己的使用者名稱，代表設定成功

```cmd
ssh -T git@github.com
```

![alt tag](https://i.imgur.com/rdLf4iX.png)

```cmd
ssh -T git@blue.github.com
```

![alt tag](https://i.imgur.com/YTNHPfN.png)

ya :heart_eyes: 我們設定成功惹~

如果有問題，也可以用 debug 模式看問題出在哪裡，通常是 `config` 輸入有誤

```cmd
ssh -vT git@github.com
```

接下來先和大家說明一下，

```cmd
git config --global user.name "blue-rubiks"
git config --global user.email "blue555236sa56@gmail.com"
```

`--global` 顧名思義就是全域的意思，如果沒輸入，就代表是目錄底下的 repo 會生效，

現在我們 clone 一個 repo 來玩玩看 (你可以自己建立一個)

```cmd
git clone git@github.com:blue-rubiks/github-ssh-test.git
```

接著，切換到目錄資料夾底下，輸入以下指令

```cmd
git config user.name "blue-rubiks"
git config user.email "blue555236sa56@gmail.com"
```

注意，這邊沒加上 `--global`，所以只有該目錄底下的 repo 會生效，

我們找到 repo 中的 `.git` 資料夾 , 再找到 `config` 檔案，內容大致如下

![alt tag](https://i.imgur.com/vT6GiYR.png)

主要就是修改第 9 行成第 10 行，修改為你設定的 `Host`，

最後，可以安心 commit 以及 push 了。

如果你真的聽不懂我在說什麼，建議看影片說明，我會帶大家操作一波 :laughing:

## 執行環境

* Win 10

## Reference

* [Multiple SSH Keys settings for different github account](https://gist.github.com/jexchan/2351996)

## Donation

文章都是我自己研究內化後原創，如果有幫助到您，也想鼓勵我的話，歡迎請我喝一杯咖啡:laughing:

![alt tag](https://i.imgur.com/LRct9xa.png)

[贊助者付款](https://payment.opay.tw/Broadcaster/Donate/9E47FDEF85ABE383A0F5FC6A218606F8)

## License

MIT licens