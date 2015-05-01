---
layout:		post
title:		"CC1:Google App Engineを使ってみた"
date:		2015-04-20
category:	blog
---
研究課題は何をしようか全然思いつかなかった時、大学の講義を見て、「クラウド◯◯」「クラウド◯◯◯◯」のようなタイトルばかりだから、とにかくクラウドを勉強しようと決めた。
<br><br>
授業でいろいろな単語が出た。まずは実践できそうなことを書いて、いちいち試してみよう。
<br><br>
OpenStack<br>
Google App Engine<br>
Amazon EC2<br>
Windows Azure<br>
heroku<br>
git<br>
…
<br><br>
ということで、前日からGAEの<a href="https://cloud.google.com/appengine/docs/java/gettingstarted/introduction">Javaチュートリアル</a>をやってみた。
<br><br>
自宅環境：
MacBook Air (13-inch, Early 2015)
OS X Yosemite 10.10.3
<br><br>
まずはjavaとMavenのインストールだ。Java（1.7.0_75）はインストールした経験があるから、すぐ出来た。でもMaven（3.3.1）をインストールする途中で問題が起きた。mvnコマンドが実行できなかった。その後Maven(3.2.5)もインストールしてみたが、問題なくできた。<a href="http://qiita.com/ringo/items/db58b34dc02a941b297ff">調べてみる</a>と、OS XはもともとAppleが提供しているJavaインストールしておいたようだ。環境変数JAVA_HOMEを設定して、問題を解決した。
<br><br>
次はチュートリアルに従って無事に終わった…と言いたいけど、このチュートリアルはいくつの必要な手順を記載していない。幸いprojectのsourceがダウンロードできるので、なんとなく出来た。
<br><br>
最後アップロードして、success codeを入力するとき、グーグルアカウントを間違えた（二つ持っている）。多分そのため、ずっと”This application does not exist”というエラーが起きて、アップロードできなかった。もう一度入力しようと思うけど、(This information is remembered after you do it once)という原因で、直る方法が見つからなかった。そしてここを開きなおして、間違えたアカウント新しいプロジェクトを作って、my-app-idを変更して、再度アップロードしてみた。今度は“version does not match expression”というエラーが出た。残念ながらまだ解決する方法が分からない。
<br><br>
Google App Engineの試しを一旦やめて、明日からWindows Azureとかherokuとかやってみようと思う。それに、来週の金曜の授業まではgitを使いこなさなければならない。Amazon EC2はクレジットカードの申し込みができたらやろう。
<br><br>
追記:今日プログラムを簡略化して、アップロードはようやく出来ました。今後もこれをベースとして、GAEでjavaプログラムを書いてみようと思う。
