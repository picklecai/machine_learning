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

