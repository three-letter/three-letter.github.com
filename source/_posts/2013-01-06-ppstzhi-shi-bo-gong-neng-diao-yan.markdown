---
layout: post
title: "PPST之视播功能调研"
date: 2013-01-06 16:35
comments: true
categories: 
---

### 视播功能的基本需求

在PPST中视播功能应该包含以下两个：

1）视频播放，包括：外观、播放、暂停、停止、声音调节、全屏等

2）限时试看，能够在一定条件下限制视频资源的试看时间


### 媒体播放器jPlayer

[jPlayer]是一款非常优秀的基于jQuery的HTML5开源播放器，支持音频和视频，同时提供了2套非常fashion的皮肤。

通过官网的[dev guide]能快速上手，其强大的功能完全能够满足视播的需求


1）构建一个jPlayer播放器

其中有几个需要注意的设置：播放器支持的格式， 视频资源、jPlayer提供的swf、视频海报(封面)的路径，具体可参考如下：

	$("#jquery_jplayer_1").jPlayer({
		ready: function () {
			$(this).jPlayer("setMedia", {
				ogv: "assets/Big_Buck_Bunny_Trailer.ogv",
				poster: "http://www.jplayer.org/video/poster/Big_Buck_Bunny_Trailer_480x270.png"
			});
		},
		swfPath: "assets",
		supplied: "ogv",
		size: {
			width: "640px",
			height: "360px",
			cssClass: "jp-video-360p"
		}
	});


2）限时试看

jPlayer提供了事件 绑定及相关功能，查询[dev guide]后可以很清楚的发现timeupdate事件能满足限时试看需求，描述如下：

	$.jPlayer.event.timeupdate * Occurs when the currentTime is changed. (~250ms between events during playback.)

实现原理及方法：jPlayer播放视频时，绑定其timeupdate事件，在指定条件下(如：限时试看5s)触发对应的功能(如：暂停播放、将视频播放时间回调至5s、显示提示信息)，具体代码如下：

	$("#jquery_jplayer_1").bind($.jPlayer.event.timeupdate, function(event){
		var cur = event.jPlayer.status.currentTime;
		if (cur > 5){
			$(this).jPlayer("pause", 5);
			$("#play-a").click();
		}
	});


3）demo展示

通过以上方法就能轻松实现视播的基本功能，通过[点击这里]查看demo。

ps:demo部署在heroku(国外的云平台)上，可能会有点卡或慢。


[jPlayer]: http://www.jplayer.org

[dev guide]: http://www.jplayer.org/latest/developer-guide

[点击这里]: http://ppst-demo.herokuapp.com/home/index
