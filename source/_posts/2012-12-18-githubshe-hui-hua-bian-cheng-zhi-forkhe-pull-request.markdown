---
layout: post
title: "github社会化编程之fork和pull request"
date: 2012-12-18 14:24
comments: true
categories: github fork pull git
---

在社会化编程上，[github]让程序员间协同工作变得更加简单有趣。
通过对[fork]和[pull request]的基本应用对github社会化编程有个清晰的认识。
  
### Fork

#### 1.创建项目分支

在目标repo详细页的右上角有个Fork按钮，点击后提示"fork the repo",等待几秒后跳转至该repo详细页。

#### 2.克隆之前创建的项目分支至本地

	git clone git@github.com:yourname/yourforkproject.git

#### 3.配置远程连接

	git remote add upstream https://github.com/owen/project.git
	# 添加一个名为upstream的目标项目远程连接
	git fetch upstream
	# 获取目标项目的更新代码至本地

### Pull Request

#### 1.提交修改至项目所有者

通过github项目分支的详细页右上角Pull Request按钮，确认该request的标题和描述后即可提交。当然也可查看具体修改的文件信息内容。

#### 2.项目所有者查看修改

有以下两种方式：

所有的修改请求都会发送邮件至所有者的github注册邮箱，里面有修改信息和对应的链接，点开即可查看。

在原始项目的详细页上面的工具栏中Pull Requests(123)出显示了全部的待合并的修改。
项目所有者点击进去查看，可根据修改的有效性进行合并或直接关闭


#### 3.合并有用的修改

若修改没有冲突，github会提示"This request can be automatically merge",那么直接点击后面的Merge Pull Request按钮即可合并

若存在冲突，github会提示"Thoes request can't be automatically merge"，后面也不存在Merge Pull Request按钮，需要手工合并
通过以下方式合并：

	cd project
	git remote add forker git://github.com/forker/project.git
	# 这里的远程连接指定的是git read-only地址
	git fetch forker
  # 获取指定forker所有的已提交修改
	git merge forker/master
  # 会提示automatically merge fail
	git status
  # 打开对应的文件手工合并即可
	git push 
  # 合并完成后提交github


[github]: https://github.com/
[fork]: https://help.github.com/articles/fork-a-repo
[pull request]: https://help.github.com/articles/using-pull-requests


