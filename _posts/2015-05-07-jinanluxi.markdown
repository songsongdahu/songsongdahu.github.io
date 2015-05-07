---
layout:		post
title:		"jinanluxiのウェブサイトをAmazonEC2に移った"
date:		2015-05-07
category:	blog
---
<a href="https://github.com/songsongdahu/jinanluxi">ソース</a><br>
<a href="http://www.jnluxi.net/Html/Main.asp">old site</a>
<a href="http://52.68.167.127:8080/jinanluxi/">new site</a>
###背景
jinanluxiという会社のサイトは、もともと他のプログラマー（会社?）を依頼してaspで書かけれました。今回は、このサイトをjspで書き直して、先日構築したAmazonEC2のサーバーに移りました。もちろん、サイトのデザインをそのままにして、バックエンドだけ変えました。<br>

###開発環境
java 1.7.0_75<br>
Tomcat 7.0.61(サーバー側はtomcat8だけど問題なく使える)<br>
MySQL 5.6.24<br>
Sublime Text Build 3083<br>

コンパイルするとき、tomcatインストールディレクトリの中のlib/servlet-api.jarがよく使われているから、環境変数CLASSPATHに添加しました。<br>

###servletとjspパラメータの受け渡し
jspからservletへ<br>
1.formタブを用いる（getまたはpost）<br>
2.urlに?name=valueを追加する（get）<br>

servlet:request.getParameter("name");<br>

servletからjspへ<br>
servlet:request.setAttribute("name",value);<br>
jsp:(valueのデータ型)request.getAttribute("name");<br>

valueのデータ型はなんでもおｋだと思います。<br>

ちなみに、servletからjspへのforwardは以下のように書きます。<br>
request.getRequestDispatcher("url").forward(request, response);

###データベース
MySQLを使いました。JavaとMySQLの接続は<a href="http://dev.mysql.com/downloads/connector/j/">Connector/J</a>を使いました。<br>

またjavaとmysqlの接続方法を忘れた時、<a href="https://github.com/songsongdahu/jinanluxi/blob/master/WEB-INF/classes/DBHelper.java">DBHelper.java</a>を参考すれば良い。<br>

sqlの書き方もだいたい忘れちゃいましたので、とても有名なw3schoolsのチュートリアルを参考しました。<br>

mysqlのバックアップはここに<a href="http://phpspot.net/php/pgmysqldumpでバックアップ＆復元.html">参照</a>。<br>

ちなみに、データベースの遠隔操作まだできません。しばらくは、ローカルからバックアップしてサーバーに復元することになっています。

###to do
1.ページング<br>
2.imgをそのまま使っていますので、サイズがデカすぎてロードは遅くなっています。<br>
3.コンソール(ただしweb上のテキストエディタはどうするかまだ分からない)

