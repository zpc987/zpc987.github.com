---
layout: post
category : program
tags : [emacs]
---

#### 如何不重新启动 Emacs 就让 .emacs 的配置起作用(4种方法都可以)

1. 用 emacs 打开 .emacs 文件，C-x C-e 光标前面的运行一条语句。立即生效。  
2. 选择一个 region , M-x eval-region  
3. M-x load-file ~/.emacs  
4. M-x eval-buffer  
都是立即生效，可以马上试验一条语句的效果。 例如，在任何一个文件中，写  
` (setq frame-title-format "emacs@%b") ` 
把光标停在在这条语句后面， C-x C-e ，马上看到 emacs 的 标题栏上发生变化。

---

#### gdb  
命令                 功能   
gdb                  启动gdb进行调试   
gdb-many-windows     切换单窗格/多窗格模式   
gdb-restore-windows  恢复窗格布局  
  
设置断点，控制程序流程 4.1 设置、删除断点  
首先将断点设置在要调试的地方。有两种方法：  
第一种，在要设置断点的行左边的fringe上单击一下（就是文本左边与滚动条之间空出的那一块）。隐藏了fringe的朋友可以M-x fringe-mode显示它。  
第二种，使用默认快捷键` C-x C-a C-b `, 或者` C-x <SPC> `。它们都关联到命令gud-break。  
无论使用哪种方法，fringe上都会在设置了断点的行上显示一个红点，表示这行设了断点  

---

#### 在每行行尾加入指定字符

	replace-regexp $ 字符
用正则表达式来替换

	C-M-S-5 
	$ 
	string
    
---

#### Emacs 中的鼠标滚轮翻阅设置
1. 最好的办法是在Customize中设置mouse wheel的 Mouse Wheel Scroll Amount.
把其值设为鼠标滚动一次想要翻过的行数。还可关闭Mouse Wheel Progressive Speed.

2. 另一种办法是在.emacs中定义函数，并把该函数绑定给鼠标滚轮的上翻与下翻动作（分别是mouse-4与mouse-5).

		;; the following function is to scroll the text one line down while keeping the cursor
		(defun scroll-down-keep-cursor ()
		(interactive)
		   (scroll-down 1))
		
		;; the following function is to scroll the text one line up while keeping the cursor
		(defun scroll-up-keep-cursor ()
		(interactive)
		   (scroll-up 1))
		
		;; binding mouse-4 and mouse-5 to the above two functions
		(global-set-key [mouse-4] 'scroll-down-keep-cursor)
		(global-set-key [mouse-5] 'scroll-up-keep-cursor)
这种方法有个小问题，即当是多窗格情况，滚轮翻动的始终是光标焦点所在的窗格，而不是鼠标所指向的窗格。

3. .emacs中加入

		(setq mouse-wheel-scroll-amount '(1 ((shift) . 1)((control)))
		mouse-wheel-progressive-speed nil
		scroll-step 1)

---

#### Emacs编码设置

**来用指定的编码重新读入这个文件.**
C-x RET r ( M-x revert-buffer-with-coding-system)  

**不改变当前文件编码，但将该文件另存为utf-8编码格式:**
C-x RET c(M-x universal-coding-system-argument ) utf-8  
（universal-coding-system-argument:用给定的编码系统执行一个I/O命令）


**emacs判断文件编码的过程/出现乱码的原因**
[from](http://blog.waterlin.org/articles/set-emacs-default-coding-system.html)  
假设一个文件是gbk编码的，emacs打开文件时首先根据一个包含了许多编码系统的列表（这个列表可以用M-x describe-coding-system看到）依次进行判断，从第一个到最后一个，直至遇到能够识别gbk编码的编码系统才停止。只要列表中含有gbk，那么就可以正常识别；但是若在遇到gbk之前就有其他的编码系统识别该文件（比如latin-1，这个编码系统的识别范围很大），就会出现乱码。所以这个列表的第一项应该是最常用的文件编码比如utf-8（可以通过M-x prefer-coding-system选择或者在.emacs里加上(prefer-coding-system 'utf-8)保存选择）。

#### 转换文本编码
在linux下：

	file xxx
	iconv -f GBK -t UTF-8 xxx -o xxx

#### 打开tex结尾的文件时默认用gbk编码。
~/.emacs 配置里加入下面以句

	(modify-coding-system-alist 'file ".*\\.tex\\'" 'chinese-gbk-dos)

#### 怎样在每行行尾加入指定字符
` replace-regexp $ YOUR_CHAR `

#### align-regexp 按照某一符号对齐
使用` C-M-\ `一般可以完成排版要求。
使用` align-regexp `可以使选中的代码按照某一指定字符（可以是正则表达式）对齐。

#### occur 和 re-builder
输出 BUFFER 中符合正则表达式的所有行，与vim中` [I `的作用差不多。  
re-builder直接在本文件中高亮，occur会另外打开一个buffer。

#### apropos
搜索包含某关键字或者匹配某正则表达式的 Emacs 命令，利用这个可以发现更多给力的 feature。

#### follow-mode
竖分屏后执行 follow-mode，所有 buffer 显示同一文件的不同部分。

#### wdired-change-to-wdired-mode
在 dired-mode 使用该 mode，就可以像文件那样对 dired-mode buffer 进行编辑，可以用 regex-replace，rectangle 命令，批量更改文件名等。

#### 切换buffer的利器
[ido-mode](http://emacswiki.org/emacs/InteractivelyDoThings)  
[iswitchb-mode](http://www.emacswiki.org/cgi-bin/emacs-en/IswitchBuffers)  
作用相似，选取一个就可以了。

#### 加载插件的时候，使用(add-to-list 'load-path "~/.emacs.d")不起从用
加上(require 'dove-ext)或者可以指定要加载的文件(load "~/.emacs.d/dove-ext.el")

#### stop search after file ending，not wrap search
(setq isearch-wrap-function (lambda () (error "no more matches")))

#### 使search可以像vim一样智能
emacs的search比较笨，vim的\*和#可以自动匹配光标下的整个word。使用这个插件：  
[highlight-symbol](http://nschum.de/src/emacs/highlight-symbol/)  
按键按照自己的喜好设置，我的设置如下：  

	(global-set-key [(s f9)]    'highlight-symbol-at-point)
	(global-set-key [(s f10)]   'highlight-symbol-next)
	(global-set-key [(s f11)]   'highlight-symbol-prev)
	(global-set-key (kbd "s-s") 'highlight-symbol-prev)
	(global-set-key (kbd "s-r") 'highlight-symbol-query-replace)


#### Emacs 中的 Undo/Redo
vim可以使用` u `和` C-r `来实现undo和redo，Emacs只有undo，没有redo。  
Emacs把redo看成是对undo的undo。只要` C-f `，之后的undo被认为是redo。

#### [evil](http://emacswiki.org/emacs/Evil) 插件
模拟vim的插件，从vim转过来的user一定要装。  
至少有些vim的功能我们还没能在emacs实现的时候，这是一个好的解决办法。学会自己写插件时，再把相应功能用elisp实现。

#### emacs 中 shell 下的命令

	C-c C-c ：终端当前作业
	C-c C-d ：送出EOF字符
	C-c C-u ：删除当前行
	C-c C-o ：删除最后一条命令的输出
	C-c C-r ：把输出内容第一行移动到文件顶部
	C-c C-e ：把输出内容最后一行移动到文件顶部
	C-c C-p ：移动到前一条命令
	C-c C-n ：移动到后一条命令
	
#### 有用的移动命令

	M-m ：移动到当前行的第一个不是空白符的位置
	M-^ ：将当前行拼接到上一行

#### [emacs 中目录的操作](http://blog.csdn.net/pfanaya/article/details/6967929)


### emacs 的一些比较好的博文

1. [Emacs 不流行但很拉风的 Feature](http://blog.zhengdong.me/2011/03/31/emacs-features/)
2. [Emacs 中的查找](http://ann77.emacser.com/Emacs/EmacsSearch.html)
3. [一年成为Emacs高手](http://blog.csdn.net/redguardtoo/article/details/7222501)
