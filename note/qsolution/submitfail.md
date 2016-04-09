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


