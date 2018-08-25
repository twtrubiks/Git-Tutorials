# Git-Flow  基本教學  :memo:

[Git-Flow Tutorials - youtube](https://youtu.be/zXlta66thZY)

[Git-Flow SmartGit Tutorials - youtube](https://youtu.be/ualXHytifbg)

在開始要了解 Git-Flow 之前，建議大家先對 Git 有基本的認識，

可以參考我之前寫的 [Git-Tutorials GIT基本使用教學](https://github.com/twtrubiks/Git-Tutorials)

## 什麼是 Git-Flow

在 Git 中有很多指令， 如果你使用 Git-Flow ，會多一些額外的功

能，但這先功能都只是由基本功能下去組合出來的，講簡單一點

，就是 A = B + C + D 的概念 ，當然，也不用擔心需要額外記指令

，有 GUI 介面 ( 有很多套可以使用，我是使用 [SmartGit](http://www.syntevo.com/smartgit/) ) ，而且很方便。

## 為什麼要使用 Git-Flow

當你一個人在用 Git 的時候一定很爽，你想怎麼 commit 或

者怎麼 merge 甚至在哪個分支下開發你都可以自己決定，但

如果是多人共同開發呢 ？ 每個人都有自己的習慣，這樣豈不

是天下大亂，於是 Git-Flow 就產生了。

## Git-Flow 並不是一個新技術，他只是一個規範

很多人第一次看到 Git-Flow 都會想，哇！這個什麼東西阿，好潮

哦之類的，但他只是 **一種規範** ，並不是一種新技術，當一整個

團隊都遵守某一種工作流程，比較不會發生問題。

Git-Flow 是訂出來的一種規範，如果你或公司對 Git 非常了解，

你們也可以自己定義屬於你們自己的 Flow ，不要遵守 Git-Flow ，

是完全不會有衝突的。

## Git-Flow Model

 在 Git-Flow 中，有兩個主要的分支：

***Master***

這個分支是非常穩定的，任何時刻都是 production-ready ，包含最新的 release ，也就是產品的原始碼，當任何一個人使用你的產品，第一眼看到的都是 master，**我們不能直接在 master 分支上進行任何的 commit ，只能從 Release 或 Hotfix merge 回來**。

***Develop***

開發中的分支，develop 分支是由 mater 分支分出來的，該 ( develop ) 分支提供整合不同即將 release 的 feature ( 功能 ) ，所以該分支有可能不穩定 ( 有bug ) 。通常我們也不會直接在該分支下 commit，而是透過 merge 的方式將 feature ( 功能 ) merge 進來。

Master 以及 Develop 這兩個分支非常重要，理論上要保護好這兩個分支，避免被意外刪除。

除了 **Master** 以及 **Develop** 這兩個分支之外，Git-Flow 還提供其他的分支：

***Feature***

功能開發，該分支是由 develop 分支分出來的，最後會被合併回 develop 分支。舉個例子，假設目前有 A 和 B 兩個功能經由兩個人下去開發，這兩個人會分別從 develop 分支分 A 和 B 兩個分支出來，當完成後，再 merge 回 develop 。

***Release***

當我們認為 develop 已經是一個很穩定的版本時，我們會進入 release，該分支是由 develop 分支分出來的。通常我們會在該分支底下再做一次全面的測試以及上線前的準備 ( 發佈版本的記錄 )，完成 release 後，我們會 merge 回 master 以及 develop。

***Hotfix***

該分支是由 master 分支分出來的，通常是已經上線了，但突然發現一個非常緊急的 bug ，這時候我們就會開一個 Hotfix 出來修復該 bug ，完成後我們會再 merge 回 master 以及 develop。

## 使用 SmartGit 來完成 Git-Flow

類似的 GUI 介面有很多，大家可以找適合自己的使用，我在這邊用  [SmartGit](http://www.syntevo.com/smartgit/) 介紹。

### 安裝 SmartGit

請到  [SmartGit](http://www.syntevo.com/smartgit/)  下載符合自己的作業系統，

安裝基本上不會有甚麼問題，比較需要注意的地方是如果你是非商用版，

請選擇非商用 ( 如下圖 ) ，假如是商用版，請購買 License

![](http://i.imgur.com/Qo6iy0l.jpg)

設定一些東西即可完成

![](http://i.imgur.com/thRWcvv.jpg)

進到 SmartGit 後，請先選好專案，接著我們按  Git-Flow 的圖示 ( 如下圖 )

![](http://i.imgur.com/MbJPEIF.jpg)

通常我們  Git-Flow Type 會選 **Full** ， 也就是完整的分支

![](http://i.imgur.com/xnUn9vS.jpg)

你會發現左下角的兩個主要分支跑出來了

![](http://i.imgur.com/XfWWByZ.jpg)

如要新增任何的 Feature 或  Release ，可以點選  Git-Flow 的圖示

![](http://i.imgur.com/0147G33.jpg)

更多詳細的介紹可參考

[Git-Flow SmartGit Tutorials - youtube](https://youtu.be/ualXHytifbg)

## Reference

* [gitflow](https://github.com/nvie/gitflow)

## Donation

文章都是我自己研究內化後原創，如果有幫助到您，也想鼓勵我的話，歡迎請我喝一杯咖啡:laughing:

![alt tag](https://i.imgur.com/LRct9xa.png)

[贊助者付款](https://payment.opay.tw/Broadcaster/Donate/9E47FDEF85ABE383A0F5FC6A218606F8)

## License

MIT license
