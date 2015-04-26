---
layout:		post
title:		"Amazon EC2を用いて小さいサーバーを構築してみた"
date:		2015-04-26
category:	blog
---
先日やっと使えるクレジットカードをもらいました。
今日はちょうど時間があって、すぐ登録してから使用してみました。
（研究テーマまだ全然何するかわからないのにこんなことやって本当にいいのかよ）
とにかく、下記のことをやりました。
<br><br>
###Amazon EC2の登録とインスタンスのラウンチ
登録はクレジットカードが必要なため、今日まで引き伸ばしてしまいました。インスタンスはUbuntu Server 14.04 LTS (HVM)を選びました。この<a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html">ガイド</a>に従って、すぐ終わりました。ただし、ボリュームの追加は必要ではなさそうな感じですから、してませんでした。
<br><br>
後はインスタンスへのコネクトです。上のガイドより、作成されたKey Pairをダッシュボードに登録した後、SSHでコネクトできます。コマンドはこんな感じです。
<code>ssh -i admin-key-pair-tokyo.pem ubuntu@52.68.167.127</code>
<br>毎回鍵のアドレスを入力するのは面倒臭いですから、~/.ssh/configに下のコードを追加しました。
<pre><code>
Host amazon
    HostName [インスタンスのアドレス]
    User [インスタンスのユーザーネーム]
    IdentityFile [鍵のアドレス]
    Port 22(sshだから22)	
</code></pre>
こうしたらコマンド<code>ssh amazon</code>が上の長いコマンドと同じ意味になっています。
###JavaとTomcatのインストール
Javaはapt-getコマンドを使ってopenjdk-7-jreとopenjdk-7-jdkをインストールしました。Tomcatは直接wgetコマンドを使ってTomcatの公式サイトからダウンロードしました。インストールは<a href="http://homepage1.nifty.com/y-osumi/works/code/tomcat7/">ここ</a>に参照しました。
<br><br>
しかし、こうした後外からアクセスはまだできません。EC2のダッシュボード->Security Group->使っているSecurity Groupを右クリックして->インバウンドルールの編集->ルールの追加->カスタムTCPルール ポート範囲8080->保存した後、やっと外からのアクセスはできるようになりました。（どうしてカスタムTCPルールを選んだかまだ分からない）
<code>http://52.68.167.127:8080</code>
<br><br>
ちなみに環境変数の設定はまだしていません。
###Git Remote Serverの構築
構築した後あんまり必要できないと気づいたんですけど、一旦ここに書いておきます。
<br>参照：
<br><a href="http://qiita.com/KazuyoshiUeno@github/items/bed591f7a076cb92ed20">EC2＋gitリモートサーバ構築#1</a>
<br><a href="http://qiita.com/KazuyoshiUeno@github/items/14afe3712ff43a01da69">EC2＋gitリモートサーバ構築#2</a>
<br>実は上のURLを参照する前にも構築は出来ましたけど、利用方法が間違えました。最初はpushした後、サーバー側にもローカルと同じのファイルが作成されると思いますが、多分そうではありません。サーバーから他の場所にpullしたら同じのファイルが作成されますけど…

###感想
やっぱりこのような文章はやりながら書くほうがいいと思います。