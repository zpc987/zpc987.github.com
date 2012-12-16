---
layout: post
category : program
tags : [vim]
---
使用vim的时候，总是按ESC键会比较麻烦，因为比较远，我们可以把它
和caps lock键的功能换一下，在X环境下，可以使用这个方法：

	用户根目录下建立一个.Xmodmap文件
	\>.Xmodmap
	加入下面代码
	remove Lock = Caps_Lock
	keysym Escape = Caps_Lock
	keysym Caps_Lock = Escape
	add Lock = Caps_Lock
重启电脑。OK！
