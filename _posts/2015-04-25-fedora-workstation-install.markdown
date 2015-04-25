---
layout:		post
title:		"USBメモリでfedora workstationをインストールした"
date:		2015-04-25
category:	blog
---
最初はMacBook Airでfedoraをインストールしたいと思ったけど、<a href="http://refit.sourceforge.net">rEFIt</a>というBoot Manage Softはどうしてもインストールできないため（<a href="http://ja.stackoverflow.com/questions/9067/refitが起動できない">スタックオーバーフローにも質問してみた</a>）、学校からもらったWindows PCでインストールすることにした。
<br><br>
用意するものリスト：<br>
usbメモリ 8GB<br>
Windows PC 一台（windowsがすでにインストールされた）<br>
インターネット接続できる環境（いろいろなダウンロードが必要だ）<br><br>

まずは<a href="https://getfedora.org/ja/">fedora</a>と<a href="http://sourceforge.net/projects/win32diskimager/">ImageWriterのダウンロード</a>だ（ここは「だ」をついたらなんか変な感じがするけど、省略したら多分文法が間違うかな）。ダウンロードした後、ImageWriterをインストールして、開いて、ダウンロードしたfedoraのisoイメージをusbに書き込んだ。
<br><br>
次はパーティションのチェック
