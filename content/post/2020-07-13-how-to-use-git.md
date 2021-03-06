+++
title = "Git をどう使うか"
author = ["515hikaru"]
date = 2020-07-13T23:00:00+09:00
tags = ["Git"]
draft = false
stylesheet = "post.css"
+++

## Git の使い方 {#git-の使い方}

みなさん Git どう使います？

というのも、今日 Git の話になってふと考えたのです。Git ってもちろん分散型バージョン管理システムなので、個々人のローカルリポジトリをどう管理しているのかなんてわからないなと。

おそらく中央リポジトリとして使われている Git ホスティングサービス（GitHub, GitLab, Bitbucket etc...）での運用はチームなり組織なりで決まっているでしょうけど、そこで見えているのは Git を使っている一部の側面でしかないはずなんですよね。

で、人に聞く前に自分はどうしているんだろうなとシャワー浴びながら考えていたら、妙な使い方をしているなと自分でも思ったので少し書き出してみます。


## 基本的な操作 {#基本的な操作}

ちなみに、先に例外として magit を使うケースを挙げておきます。magit は Emacs から Git 操作できる Emacs のパッケージです。ごく一部 Emacs で編集するプロジェクトがあって、そのリポジトリの Git 操作をするときは magit を使っています。このブログも Emacs で書いているので magit を使っています。ただ magit は diff/add(-p)/commit/push くらいにしか使わないです。


### commit {#commit}

コマンドラインでしかやりません。=git commit -m "commit message"= とうってコミットします。VSCode とかでコミットすることがないとは言いませんが、ごくまれです。


### ブランチ切り替え {#ブランチ切り替え}

9割くらい `git switch` で。稀に VSCode でクリックして切り替えることも。


### push/fetch {#push-fetch}

リモートリポジトリと通信するのはコマンドラインからやります。

```nil
git fetch -p --all
git rebase origin/master
```

などとするのが常です。


### diff/log {#diff-log}

基本的には \`git diff\` や \`git log\` で足りるならそれで済ませます。ただいろんな diff を見たいときは `tig` コマンドを使うこともあります。

特に「どこまで add したっけ……？」とわからなくなることがよくあるので、 Staged diff をみるために `tig` を叩くことは多いです。


### blame {#blame}

GitHub で見ます。特に工夫はありません。


### add {#add}

結構多岐に渡ります。基本は `git add -p .` をすることが多いです。1行だけ add したいときがまれにあり、そういうときは `tig` で `1` とうつと1行 add できるのでよく使います。

VSCode でも指定した範囲を add することができるので稀に使います。


### 対話的 rebase {#対話的-rebase}

`git rebase -i` 一択です。すごい頻繁にやります。


### コンフリクト解消 {#コンフリクト解消}

ほとんどの場合、コンフリクトするようなプロジェクトは複数人で開発する場合なのでコードベースも大きいことが多いです。ということで VSCode でコンフリクト解消します。

[VSCodeでgitのconflictを解消させる話 - Qiita](https://qiita.com/penpenta/items/08b59f4b788ca2ae1c07#3-merge%E3%81%97%E3%81%9F%E9%9A%9B%E3%81%ABbranch%5Fb%E4%B8%8A%E3%81%A7conflict%E3%81%8C%E7%99%BA%E7%94%9F%E3%81%97%E3%81%A6vscode%E4%B8%8A%E3%81%A7%E7%A2%BA%E8%AA%8D%E3%81%A7%E3%81%8D%E3%82%8B%E3%81%AE%E3%81%A7%E8%A7%A3%E6%B6%88%E3%81%99%E3%82%8B)

上の記事のように Accept Incoming Change とかをクリックし、さらに追記したければその場で修正も可能なので、これを使っています。


## なんでこうなった？ {#なんでこうなった}

なんでこうなったのか、よく覚えていません。

ひとつひとつは知ったときに便利だと思って導入したものなんですが、総合すると統一感がないですね。特に tig はごく限られた用途でしか使っていないし、せっかくエディタの統合機能使っているならもっとエディタでこなせばいいじゃんという気持ちにもなります。

とはいえ今の自分はこのちぐはぐなのにこなれてしまったし、意識して変えようとしなければしばらくは変わらなそうな気がします。

コマンドラインでほとんどを済ませるのはデスクトップ Linux にまともな Git クライアントが存在しないからなんですが GitQlient とかは密かに watch していたりします。

[francescmm/GitQlient: GitQlient: Multi-platform Git client written with Qt.](https://github.com/francescmm/GitQlient)

そのうち GUI クライアントも使ってみるかもです。