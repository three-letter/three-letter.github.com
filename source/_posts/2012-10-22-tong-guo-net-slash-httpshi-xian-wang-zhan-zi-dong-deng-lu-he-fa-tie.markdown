---
layout: post
title: "通过net/http实现自动登录和发贴"
date: 2012-10-22 16:42
comments: true
categories: net/http
---
### 1. 网站的自动登录

(1)引入net/http库
	
	require 'net/http'

(2)获取登录网站后的cookie
	
	rsp    = con.post(url.path,data,{})
	cookie = rsp.response['set-cookie']

(3)一般将上述操作封装成一个login方法，返回http连接和cookie用于之后的权限操作

	def login
		url = URI.parse(url) unless url.is_a?(URI)
		con = Net::HTTP.new(url.host,url.port)
		data = "username=abc&password=123"
		rsp = con.post(url.path,data,{})
		cookie = rsp.response['set-cookie']
		head = {
			'Content-Type' => "application/x-www-form-urlencoded; charset=UTF-8",
			'Cookie'       => cookie
		}
		connection, headers = con, head
	end

### 2. 自动发贴

通过上述的自动登录获取对应的con连接和headers，实现网站的权限操作(比如发贴, 查看个人信息等)

	def post
		con, headers = login
		data = "post_title=abc&post_content=xyz&user_id=123"
		rsp = con.post("post submit action",data,headers)
		msg = rsp.body
	end
