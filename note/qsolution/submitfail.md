# 提交失败  
  

## mac环境  
运行｀submit()`，输入用户名和网页上的token，就出现这样的反应：  

	!! Submission failed: unexpected error: unterminated character string constant
	!! Please try again later.

搜索：[这里](https://learner.coursera.help/hc/en-us/community/posts/204693179-linear-regression-submit-error)表示，octave4.0有问题。  

解决办法之一：  
在lib里分别找到这两个文件： loadjson.m and makeValidFieldName.m

It seems that the conversion from ASCII to the hexadecimal escape the jsonlib uses is not working properly anymore in Octave 4.0. You can get it fixed by replacing

	str=[str str0(pos0(i)+1:pos(i)-1) sprintf('_0x%X_',str0(pos(i)))];
by

	str=[str str0(pos0(i)+1:pos(i)-1) sprintf('_0x%X_',toascii(str0(pos(i))))];
and

	str=sprintf('x0x%X_%s',char(str(1)),str(2:end));
by

	str=sprintf('x0x%X_%s',toascii(str(1)),str(2:end));

替代完，好像没看见好转。

突然发现，自己的错误和上面那个页面里提的错误不一样，我只看了前半段。怪不得不能解决问题。  

想起来了，最初的错误是这个：  

	!! Submission failed: unexpected error: urlread: HTTP response code said error
	!! Please try again later.

那么上面贴的错误，应该是后来的，反正至少现在还是那个。昨天粗心，导致现在对过程迷迷糊糊的。可以肯定的是，现在3.8版本，仍然在`unterminated character string constant`错误中。  

从[这里](http://sunsite.univie.ac.at/textbooks/octave/octave_5.html)看，有点怀疑代码写错了。可是运行并未说错误，结果照常出来，都是正确的啊。

僵持了好几天，一筹莫展的情况下，去看xiaozhen的答案，发现至少第一项作业是一模一样啊，第二项作业答案也和pdf说明文档一样，写法不一样。  

晚上又换个思路，去研究lib里的提交程序。定位到出错地点：  

	  try
	    response = submitParts(conf, email, token, parts);
	  catch
	    e = lasterror();
	    fprintf( ...
	      '!! Submission failed: unexpected error: %s\n', ...
	      e.message);
	    fprintf('!! Please try again later.\n');
	    return
	  end

顺着这条去读其他的，没觉得哪里不对。顺便说一句，在[这个页面](http://zhidao.baidu.com/link?url=5YH2yFzvk1RCDLcttN9Lhowr7QVkCPqBHgo5DEuEcBUOia4NrHN6US1iLmNzsT9EHFO2312TtucfRuPtQXGxKa)上看到了对错误信息的解释：  

> 字符串或字符常量缺少结束符unterminated string or character constant 

> 检查所有字符串是否都用双引号括起来的，字符常量用单引号括起来
 
心想虽然是c语言，估计也是这类错误。但是自己写的程序作业，和标准答案核对过啊，因为从第一项想提交就是这样的，所以要是有丢失结束符的情况，也不在自己作业部分。  

这样想了，突然想到我白天已经把所有的作业都下载了，不妨试试ex2，虽然还没做。  

轰轰然，ex2，输入`submit()`后，输入email，输入token，出来的不是错误信息，而是各项作业列表：  

	==
	==                                   Part Name |     Score | Feedback
	==                                   --------- |     ----- | --------
	==                            Sigmoid Function |   0 /   5 |
	==                    Logistic Regression Cost |   0 /  30 |
	==                Logistic Regression Gradient |   0 /  30 |
	==                                     Predict |   0 /   5 |
	==        Regularized Logistic Regression Cost |   0 /  15 |
	==    Regularized Logistic Regression Gradient |   0 /  15 |
	==                                   --------------------------------
	==                                             |   0 / 100 | 
	
所以确凿无疑了，ex1的文件有问题。自己知道改的，就是上面那个改法。但submit本身有没有问题，也不确定。于是重新下载ex1，替换了lib文件夹，替换了submit程序（为什么不一项一项来呢？那样还能定位出准确错误），再提交，文件列表出来了。

如果是lib错误，那还是自己知道的。但未必。copy`submit`程序时，也提醒我磁盘上是新文件，刚下载的事旧文件。

总之这个坑拦路拦了这么些天，真不知道是什么时候程序被改动的。  

当然，问题解决了还是很高兴的，除了悲剧地发现第二项就没得分……

ps.万能的github告诉我：问题就出在上面的修改中。因为submit并没有修改纪录，而lib的两个文件，则退回原状。  

这个惨痛的教训告诉我，读句子要读完，不要因为前面长得像就以为是同一句话。

