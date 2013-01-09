---
layout: post
title: "PPST之行为驱动开发BDD - 1"
date: 2013-01-09 16:08
comments: true
categories: 
---

### BDD编程起航

结束基本核心需求分析，现在开始写代码了:)

基于ruby on rails进行敏捷开发,能够快速的生成原型。通过不断的使用和交互逐渐完善网站，同时采用BDD能有效保证在进行迭代开发的时候之前的代码的准确性。。

[Rspec]是使用Ruby实现BDD(Behaviour Driven Development)的一种DSL，其主要作用是描述我们对系统执行某个Case的期望行为.

[Factory\_girl]是专门用来构造模拟数据的工具，其动态和批量数据构造以及良好的对象依赖关联都成为替代传统fixture的最佳选择。


#### 构建项目

通过[rails\_apps\_composer]创建rails项目，其优点那是杠杠的。关于recipe的选择，作者推荐的是core，在这里我只用testing fontend

	rails_apps_composer list   # list all recipes
	rails_apps_composer new ppst -r models testing fontend   # require the base recipes

ps:使用的数据库为postgresql,需要更改其数据库配置信息(如：encoding)，同时在执行数据库迁移后postgresql会自动为pk生成一个连续表，可以忽略

#### BDD编程

在正式开始编程前需要完成以下配置

1）在spec\_helper.rb中为Factory\_girl增加两个配置。

	require 'factory_girl'
	config.include(FactoryGirl::Syntax::Methods)


2）根据recipe的不同选择，可能还需要在Gemfile中加下以下2个gem

	gem "shoulda-matchers", :group => [:development, :test]  # assert syntax
	gem "webrat", :group => [:development, :test]            # page selector

ok，我们先从用户中心(User)...

#### test model

生成user model时，rspec会生成2个主要文件factories/users.rb、models/user\_spec.rb

修改users.rb，使之能动态构造测试数据

	factory :user do
		name { "user_#{User.count + 1}" }
		pwd { "password_#{User.count + 1}" }
		pwd_confirmation { "password_#{User.count + 1}" }
	end

打开user\_spec.rb文件，根据不同case开始写测试代码

1）case 1: 用户对象字段name的相关验证

	subject { create(:user) }         # 通过factory构造测试数据：create = bulid + save   

	it { should validate_presence_of(:name).with_message("用户名不能为空") }
	it { should validate_uniqueness_of(:name).with_message("用户名已经存在") }
	it { should ensure_length_of(:name).is_at_least(2).with_short_message("用户名长度为2到8").is_at_most(8).with_long_mes    sage("用户名长度为2到8") }

上面描述了3个不同的样例(example),是相对比较高级的写法:)。其意思通过代码应该很容易找到，这时我们在项目的根路径下运行命令`rspec spec`，能看到以下结果

	rspec spec
	FFF
	Finished in 0.49 seconds
	3 examples, 3 failures

我们未对user model做任何处理，结果应该是预料中的，这3个example是不可能通过的。 

BDD/TDD简单讲就是在编程中通过不断重构将failture变成success，也就是传说中的r-r-g。。

现在对user model中的name添加验证

	validates :name, :presence => { :message => "用户名不能为空" },
	                 :uniqueness => { :message => "用户名已经存在" },
	                 :length => { :within => 2..8, :message => "用户名长度为2到8" }

添加完后，继续运行`rspec spec`，能看到以下结果

	rspec spec
	...
	Finished in 0.35 seconds
	3 examples, 0 failures

看到这个，说明用户的对象name的有效性验证通过。。

2）case 2: 用户权限的验证，如：通过name pwd能正确返回该用户信息

继续打开models/users.rb

	...  # other test code

	describe "user authenticate verify" do
		before(:each) do
			@user = create(:user)
			@user1 = create(:user)
		end

		it "should return user if valid name and pwd" do
			User.authenticate(@user.name, @user.pwd).should == @user
		end
		it "should return nil if invalid name and pwd" do
			User.authenticate(@user.name, @user1.pwd).should == nil
		end
	end

ps: before(:each)是指在执行describe下的每个example前执行某些操作(这里指创建2个不同的用户)

执行`rspec spec`后结果与预期一样，是不能通过的

	rspec spec
	FF
	Finished in 0.15 seconds
	2 examples, 2 failures

so,打开用户model，实现具体的用户权限功能

	# 其他方法就不写了，意思下就行
	def self.authenticate(username,psd)
		user = User.find_by_name(username)
		if user
			user = nil unless user.has_password?(psd)
		end
		user
	end

完成后，再执行`rspec spec`查看结果

	rspec spec
	..
	Finished in 0.21 seconds
	2 examples, 0 failures
	
model的基本测试主要有以上2中，具体的可参考资料

ok~ 大功告成。。。



未完待续。。。。




最后，以上是BDD编程中最基本的使用方法，关于其中的许多奇淫技巧，可以查询这两个网站：[Shoulda-matchers]、[Relish]


[Rspec]: http://rspec.info/

[Factory\_girl]: https://github.com/thoughtbot/factory_girl

[rails\_apps\_composer]: https://github.com/RailsApps/rails_apps_composer

[Shoulda-matchers]: http://rubydoc.info/github/thoughtbot/shoulda-matchers/master/Shoulda/Matchers/ActiveModel

[Relish]: https://www.relishapp.com/rspec/rspec-rails/docs
