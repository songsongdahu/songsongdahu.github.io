---
layout: post
title:  "Blog开设小记"
date:   2014-11-24
category: blog
---
###扯淡
之前就有利用github pages开设blog的想法，不过因为种种原因推迟了。昨天安装好jekyll之后，今天找到了合适的模板，经过一番自定义修改之后终于大致完成了。虽然markdown和liquid之前没有接(ting)触(shuo)过，还好简单易懂，随着之后对blog的维护慢慢熟悉就好了。这篇文章的主要目的就是把今天学习到的东西整理一下。
<br><br>
###Jekyll安装
http://jekyll-windows.juthilo.com/  
由于博主现在是windows系统，所以参照了上面这篇文章。
值得注意的是Ruby的版本要选择1.9.3的，否则会报不明的错误，网上似乎没有解决方案(参照<a href="http://stackoverflow.com/questions/16498287/jekyll-liquid-exception-cannot-load-such-file-yajl-2-0-yajl" target="_blank">这里</a>)。
<br><br>
###Github Pages
https://pages.github.com/  
创建了Github Pages之后，在jekyll theme上找到了一个适合自己的主题(<a href="http://jekyllthemes.org/themes/wangana/" target="_blank">Wangana</a>)，将其下载下来之后移动到Github Pages的项目所在的本地的文件夹内，然后publish，就可以看到模板在Github Pages上的效果了。
<br><br>
###Markdown语言和liquid语言
- Markdown的教程(现在博主还没理解出来Markdown有什么好处)
http://daringfireball.net/projects/markdown/  
http://www.jianshu.com/p/q81RER  (中文)

- liquid的教程  
https://github.com/Shopify/liquid/wiki/Liquid-for-Designers

<br>
###模板的一些自定义改变
- 大幅简洁化，只保留了个人想要的功能
- 对post内的文档分为blog和project两类
- 由于中文使用模板默认字体太难看，于是文档内使用微软雅黑字体

<br><br>
###结语
以后大概会把写的程序或者学习相关的一些东西放到这里，大概会常驻吧...请多关照>_<
