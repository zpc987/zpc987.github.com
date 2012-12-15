---
layout: post
category : program
tags : [latex,table]
---
想使用latex制作下面一个表格。

	                  LSB                         MSB	
	-------------------------------------------------+
	2 Octets  | TCI  | 0 | 0 | 0 | 0 | 0 | 1 |EoF|SoF|
	          |      |---+---+---+---+---+---+---+---+
	          |      | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
	----------+------+---+---+---+---+---+---+---+---+
	2 Octets  |LENGTH|   |   |   |   |   |   |   |   |
	          |      |---+---+---+---+---+---+---+---+
	(Optianal)|      |   |   |   |   |   |   |   |   |
	-------------------------------------------------+

<!--
<img src = "../image/latex2.jpg" >
-->
比较难制作的是上面的“LSB”和“MSB”，因为刚学习latex不久，所以想了很久，
而且在网上也很难找到答案,最终参考了《The Not So Short Introduction to 
LaTeX2e》这篇文档中的一个例子。
<!--
<img src = "../image/latex1.jpg" >
-->
使用\multicolumn命令实现。
代码如下。

	\begin{tabular}[c]{ c|c|c|c|c|c|c|c|c|c| }
	\multicolumn{2}{c}{} & \multicolumn{1}{c}{\tiny{LSB}} & \multicolumn{6}{c}{} & \multicolumn{1}{c}{\tiny{MSB}} \\
	\hline
	2 Octets & TCI & 0 & 0 & 0 & 0 & 0 & 1 & \scriptsize{EoF} & \scriptsize{SoF} \\ \cline{3-10}
	& & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 \\
	\hline
	2 Octets  & LENGTH &   &   &   &   &   &   &   &  \\ \cline{3-10}
	(Optianal) &   &   &   &   &   &   &   &   &   \\
	\end{tabular}
(画上面那个表格花了好长时间啊，T_T)
