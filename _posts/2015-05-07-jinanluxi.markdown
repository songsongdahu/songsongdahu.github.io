---
layout:		post
title:		"jinanluxiのウェブサイトをAmazonEC2に移った"
date:		2015-04-26
category:	blog
---
<a href="https://github.com/songsongdahu/jinanluxi">ソース</a>
###背景
jinanluxiという会社のサイトは、もともと他のプログラマー（会社?）を依頼してaspで書かれた。今回は、このサイトをjspで書き直して、先日構築したAmazonEC2のサーバーに移った。もちろん、サイトのデザインをそのままにして、バックエンドだけ変えた。<br>

###開発環境
java 1.7.0_75
Tomcat 7.0.61(サーバー側はtomcat8だけど問題なく使える)
MySQL 5.6.24
Sublime Text Build 3083

コンパイルするとき、tomcatインストールディレクトリの中のlib/servlet-api.jarがよく使われているから、環境変数CLASSPATHに添加した。

###データベース
MySQLを使った。JavaとMySQLの接続は<a href="http://dev.mysql.com/downloads/connector/j/">Connector/J</a>を使った。<br>
javaとmysqlの接続方法を忘れた時、<a href="https://github.com/songsongdahu/jinanluxi/blob/master/WEB-INF/classes/DBHelper.java">DBHelper.java</a>を参考すれば良い。<br>
