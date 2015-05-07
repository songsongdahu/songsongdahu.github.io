---
layout: post
title:  "LR1Item_generator(en)"
date:   2014-11-25
category: program
---
[<a href="../LR1Item-generator/">简体中文</a>]/[English]
###**Introduction**  
LR1Item_generator is a program that can be used to generate the LR(1) items and parsing table from inputted grammar.  

**Environment**  

- windows 7
- jdk1.8.0_25

<a href="https://github.com/songsongdahu/LR1Item_generator">source on github</a>  

###**InputFormat**  
- The grammar symbols should be spilt by the symbol '@'
- You should input the symbol '!' before a terminal symbol to show that it is a terminal symbol(If you don't, it will be recognized as an nonterminal symbol)
- In each line you could input only one produciton
- The input will be stopped when you input an empty line

For example, the grammar <code>S->Cab</code> will be inputted like <code>S@C@!a@!b</code> (Notice that S and C are nonterminal symbols while a and b are terminal symbols).  
  
**The way of inputting**
{% highlight java linenos %}
LR1Item G = la.readInput();
//LR1Item G = la.readTxt();
{% endhighlight %}
If you choose the first line（default）, please run the program and input the grammar in line.  
If you choose the second line, please write the grammar into "Productions.txt" before running   
p.s. I have already inputted the PL/0's grammar into "Productions.txt" ,which can be used as examples.（The program will generate 273 LR(1) items :）  
###**Examples(from <a href="http://ja.wikipedia.org/wiki/LR%E6%B3%95" target="_blank">Wikipedia</a>)**
<pre><code>Grammar:
(1)E→E*B
(2)E→E+B
(3)E→B
(4)B→0
(5)B→1


Input:
E@E@!*@B
E@E@!+@B
E@B
B@!0
B@!1

Output1:parsing table  
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

Output2:LR(1) items:
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

###**Main methods**  
- CLOSURE: return the CLOSURE set of productions
<pre><code>SetOfItems CLOSURE(I){
    repeat
        for each item {A -> α.Bβ，a} in I
            for each production B -> γ in G’
                for each terminal symbol b in FIRST(βa)
                    add {B -> . γ, b} into set I;
    until no new items will be added into set I;
    return I;
}
</code></pre>

- GOTO: return the GOTO set of productions
<pre><code>SetOfItems GOTO(I,X){
    Initialize J as an empty set;
    for each item {A -> α.Xβ，a } in I
        add item {A -> αX.β，a} to set J;
    return CLOSURE(J);
}
</code></pre>

- item: the main method to generate LR(1) items
<pre><code>void items(G’){
    Initialize C as {CLOSURE({S’->.S, $})};
    repeat
        for each item I in set C
            for each symbol X
                if GOTO(I,X) is not in C and is not null
                    add GOTO(I,X) to set C;
    until no new items will be added into set C;
}
</code></pre>