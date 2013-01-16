---
layout: post
category : program
tags : [gvim,ubuntu]
---
使用sudo gvim命令遇到“No protocol specified”，无法打开文件。是因为X server不允许root登陆造成的。解决办法：
1. try starting Vim with "-X" to tell vim not to bother connecting to the X server.  It's fast, easy, and reliable, but loses the ability for root to use the X clipboards 
	
	sudo gvim XXX -X

2. link the ~user/.Xauthority to ~root/.Xauthority with 

	ln -s ~user/.Xauthority ~root/.Xauthority 

[引文](http://vim.1045645.n5.nabble.com/vim-says-quot-No-protocol-specified-quot-and-I-have-no-idea-what-it-means-td5680529.html)
