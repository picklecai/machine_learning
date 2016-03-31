# Ocatave安装教程  


## win环境  

环境为win8.

win版下载地址：[Index of /gnu/octave/windows](https://ftp.gnu.org/gnu/octave/windows/)  

需要下载的是exe文件。  

安装时提示说不太支持win8，并需要java环境。  

硬安装了，命令行界面能打开，还不知道能不能正常跑。  

win下可正常运行。  

## mac环境  

mac版本为10.10  

[Machine Learning:Mac下安装Octave](http://mooc.guokr.com/note/15825/)  

这里不推荐ng的方法，推荐用homebrew。  

### 安装homebrew  

从[Homebrew — OS X 不可或缺的套件管理器](http://brew.sh/index_zh-cn.html)这里，获取代码，粘贴到命令行中去：  

	/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  

第一次说连接错误，第二次又重新粘贴，开始工作，中间提示输入mac密码，最后安装成功。  

### homebrew使用  

	brew help  
帮助文件  

	brew update  
检查最新版本并更新。因为刚刚安装，所以最新。  

	brew list  
用homebrew安装的文件列表。因为还没有用过，所以空。   

### 用homebrew安装octave  

	brew install octave  

结果反应非常有趣：   

	These formulae were found in taps:  
	homebrew/science/octave  Caskroom/cask/octave  Caskroom/cask/xoctave  
	To install one of them, run (for example):  
	    brew install homebrew/science/octave  

[Octave for MacOS X - Octave](http://wiki.octave.org/Octave_for_MacOS_X)这里有完整的octave安装方法。据它看，上面三个选择应该选择第一个。  

成功开始安装了之后，居然差不多一个半小时才装完，似乎是装了很多插件。最后octave的版本是4.0.0_5.