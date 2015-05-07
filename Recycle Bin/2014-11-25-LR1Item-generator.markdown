---
layout: post
title:  "LR1Item_generator(cn)"
date:   2014-11-25
category: program
---
[简体中文]/[<a href="../LR1Item-generator-en/">English</a>]
###**简介**  
LR1Item_generator是一个用来生成LR(1)项目集的程序，它以一个LR(1)文法的产生式集合作为输入，经过计算生成LR(1)的项目集以及分析表。  

**环境**  

- windows 7
- jdk1.8.0_25

<a href="https://github.com/songsongdahu/LR1Item_generator">源代码</a>  

###**输入格式**  
- 文法符号与文法符号之间使用@分隔开
- 终结符号前使用!标识
- 每一行表示一个产生式
- 空行代表输入结束

例如<code>S->Cab</code>的输入为<code>S@C@!a@!b</code>(其中S、C为非终结符,a、b为终结符)  
  
**输入方法**
{% highlight java %}
LR1Item G = la.readInput();
//LR1Item G = la.readTxt();
{% endhighlight %}
如果选择上面一行（默认），则在运行之后按行输入语法，空行结束。  
如果选择下面一行，则需要在运行前将语法预先输入到Productions.txt中。  
p.s. 当前Productions.txt默认保存了PL/0的语法，可以作为示例使用（结果会产生273个LR1项集）。  
###**示例(源自<a href="http://ja.wikipedia.org/wiki/LR%E6%B3%95" target="_blank">wikipedia</a>)**
<pre><code>文法:
(1)E→E*B
(2)E→E+B
(3)E→B
(4)B→0
(5)B→1


输入:
E@E@!*@B
E@E@!+@B
E@B
B@!0
B@!1

输出 分析表:  
--------------------This is the parsing table--------------------
	*	+	0	1	E	B	$
I0			s1	s2	s3	s4	
I1	r3	r3					r3
I2	r4	r4					r4
I3	s5	s6					
I4	r2	r2					r2
I5			s1	s2		s7	
I6			s1	s2		s8	
I7	r0	r0					r0
I8	r1	r1					r1

输出 LR(1)项集:
---------------------This is the LR(1) items---------------------
I0
S' -> .E , $
E -> .E*B , $/*/+
E -> .E+B , $/*/+
E -> .B , $/*/+
B -> .0 , $/*/+
B -> .1 , $/*/+

I1
B -> 0. , $/*/+

I2
B -> 1. , $/*/+

I3
S' -> E. , $
E -> E.*B , $/*/+
E -> E.+B , $/*/+

I4
E -> B. , $/*/+

I5
E -> E*.B , $/*/+
B -> .0 , $/*/+
B -> .1 , $/*/+

I6
E -> E+.B , $/*/+
B -> .0 , $/*/+
B -> .1 , $/*/+

I7
E -> E*B. , $/*/+

I8
E -> E+B. , $/*/+
</code></pre>

###**主要算法**  
- CLOSURE方法  返回一个产生式集合的闭包
<pre><code>SetOfItems CLOSURE(I){
    repeat
        for(I中的每个项{A -> α.Bβ，a})
            for(G’中的每个产生式B -> γ)
                for(FIRST(βa)中的每个终结符号b)
                    将{B -> . γ, b}加入到集合I中;
    until不能向I中加入更多的项;
    return I;
}
</code></pre>

- GOTO方法  返回一个产生式集合的GOTO集
<pre><code>SetOfItems GOTO(I,X){
    将J初始化为空集;
    for(I中的每个项{A -> α.Xβ，a })
        将项{A -> αX.β，a}加入到集合J中;
    return CLOSURE(J);
}
</code></pre>

- item方法  利用goto和closure生成LR1的items的主方法
<pre><code>void items(G’){
    将C初始化为{CLOSURE({S’->.S, $})};
    repeat
        for(C中的每个项集I)
            for(每个文法符号X)
                if(GOTO(I,X)非空且不在C中)
                    将GOTO(I,X)加入C中;
    until 不再有新的项集加入到C中;
}
</code></pre>