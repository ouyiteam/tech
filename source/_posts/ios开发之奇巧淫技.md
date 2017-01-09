
---
title: ios开发之奇巧淫技
author: 赵文龙
---

>作者：赵文龙

1.The file “GCZP” couldn’t be opened because you don’t have permission to
	解决办法1：将info.plist的文件中的Executable.file中的文件修改为:$(PRODUCT_NAME)
	解决办法2：删除info.plist文件，重新添加。该方法注意事项（1）不能删除引用。（2）添加时注			   意该文件的原始路径
2.状态栏背景颜色问题
	解决办法1：用系统的方法修改。
	解决办法2：写一个高为20的view。
	解决办法3：将背景y坐标向上调20。
3.导航条上重新定义titleView导致左右两边不对称或者左右两边问题
	解决办法1：重新定义左右两边按钮改变其大小。
	解决办法2：隐藏本身导航条，重新定义导航条。
4.验证某一个地址是否支持ATS，命令行代码 /usr/bin/nscurl --ats-diagnostics --verbose URL 该命令行需要满足OS X v10.11 会显示出每个请求与相应的配置当输出pass则为通过
5.与服务器对接时后台无法获取到参数
	解决办法1：如果请求没有进行序列化，请进行序列化。
	解决办法2：如果请求有进行序列化，请注释掉序列化。
6.formData表单提交时后台无法区分文件
	解决办法1：请先使用 formData appendPartWithFileData: name:
	解决办法2：如果方法1不通，请使用[formData appendPartWithFileData: name: fileName: mimeType:]; 该方法是告诉后台改文件的类型，如果没有传入文件的类型，那么后台将无法识别。
7.当某一个返回值是由block异步回调得到返回值不能直接赋值
	解决办法1：设置代理协议，进行代理回调方法赋值
	解决办法2：同意使用block回调，返回值
	解决办法3：定义block回调方法，在block回调的地方赋值该方法
8.使用时间的时候会出现8小时的误差。造成该问题的原因是我们获取的是0时区，而我们所在中国是东8区，所以会出现8小时的误差。
	解决办法1：将获取到的当前时间进行字符串化之后会得到东8区的时间。与外部交互使用该字符串时间(显示，与后台交互等)
	注意事项：解决办法1已经说明，但是在内部时需要使用0时区时间，这样就不会出现8小时误差。
8.UITableViewCell高度自适应
	注意事项：1.在代码里添加 _tableView.estimatedRowHeight = 44;
    _tableView.rowHeight = UITableViewAutomaticDimension;
		2.同时在约束里，要添加成为由内部向外部施加压力迫使contentView撑开。
		3.不能使用代理方法heightForRow返回行高，这样约束必然失效。
9.UITableViewCell宽度问题
	注意事项：先要有启动页面，这时返回宽度为320，并且布局都是按照320来，进行计算的。
	解决办法1：如果使用约束，请查看约束，因为约束可以做到，高度宽度自适应。
	解决办法2：如果使用代码布局，那么要在cell里面重写layoutSubviews方法，在里面进行		布局，即可解决问题
10.在获取view的frame时总是(0,0,1000,1000)，这是因为在iOS 10以后获取view的frame已经变化，此时布局尚未完成，所以获取不到正确的frame。viewController需要在方法viewDidLayoutSubviews里获取view的frame，或者这是view的frame。view需要在方法layoutSubviews里获取view的frame,或者设置frame。
11.在设置圆角的同时设置阴影
	因为设置圆角需要裁剪超出显示的图层，所以此时阴影是显示不出来的
	解决办法1：设置圆角记为view1，设置阴影记为view2，将view1添加到view2上，这样作为父视图，阴影将不会被裁剪掉。

