---
layout: post
title: "PPST之视播功能调研"
date: 2013-01-06 16:35
comments: true
categories: 
---

<link href="/stylesheets/player.css" rel="stylesheet" type="text/css" />
<script type="text/javascript" src="/javascripts/jquery.min.js"></script>
<script type="text/javascript" src="/javascripts/jquery.jplayer.min.js" ></script>
<script type="text/javascript" src="http://www.jplayer.org/latest/js/jquery.jplayer.inspector.js"></script>
<script type="text/javascript">

$(document).ready(function(){
		$("#jquery_jplayer_1").jPlayer({
ready: function () {
$(this).jPlayer("setMedia", {
ogv: "/assets/Big_Buck_Bunny_Trailer.ogv",
poster: "http://www.jplayer.org/video/poster/Big_Buck_Bunny_Trailer_480x270.png"
}).jPlayer("load");
},
swfPath: "/assets",
supplied: "ogv",
size: {
width: "240px",
height: "100px",
cssClass: "jp-video-360p"
}
});
		$("#jplayer_inspector").jPlayerInspector({jPlayer:$("#jquery_jplayer_1")});

		$("#btn-stop").click(function() {
			$("#jquery_jplayer_1").jPlayer("stop");
			});	

$("#jquery_jplayer_1").bind($.jPlayer.event.timeupdate, function(event){
		var cur = event.jPlayer.status.currentTime;
		if (cur > 5){
		$(this).jPlayer("pause", 5);
		$("#play-a").click();
		}
		});
});


</script>




<div id="jp_container_1" class="jp-video jp-video-episode">
<div class="jp-type-single">
<div id="jquery_jplayer_1" class="jp-jplayer"></div>
<div class="jp-gui">
<div class="jp-interface">
<div class="jp-progress">
<div class="jp-seek-bar">
<div class="jp-play-bar"></div>
</div>
</div>
<div class="jp-current-time"></div>
<div class="jp-duration"></div>
<div class="jp-controls-holder">
<ul class="jp-controls">
<li style=""><a href="javascript:;" class="jp-play" tabindex="1">play</a></li>
<li><a href="javascript:;" class="jp-pause" tabindex="1">pause</a></li>
<li><a href="javascript:;" class="jp-stop" tabindex="1">stop</a></li>
<li><a href="javascript:;" class="jp-mute" tabindex="1" title="mute">mute</a></li>
<li><a href="javascript:;" class="jp-unmute" tabindex="1" title="unmute">unmute</a></li>
<li><a href="javascript:;" class="jp-volume-max" tabindex="1" title="max volume">max volume</a></li>
</ul>
<div class="jp-volume-bar">
<div class="jp-volume-bar-value"></div>
</div>
<ul class="jp-toggles">
<li><a href="javascript:;" class="jp-full-screen" tabindex="1" title="full screen">full screen</a></li>
<li><a href="javascript:;" class="jp-restore-screen" tabindex="1" title="restore screen">restore screen</a></li>
<li><a href="javascript:;" class="jp-repeat" tabindex="1" title="repeat">repeat</a></li>
<li><a href="javascript:;" class="jp-repeat-off" tabindex="1" title="repeat off">repeat off</a></li>
</ul>
</div>
</div>
</div>
<div class="jp-no-solution">
<span>Update Required</span>
To play the media you will need to either update your browser to a recent version or update your <a href="http://get.adobe.com/flashplayer/" target="_blank">Flash plugin</a>.
</div>
</div>
</div>
<div id="jplayer_inspector"></div>		

<a href="#play-pay" id="play-a" role="button" class="btn" data-toggle="modal" style="display:none">Pay</a>
<div id="play-pay" class="modal hide fade" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
<div class="modal-header">
<button type="button" class="close" data-dismiss="modal" aria-hidden="true">×</button>
</div>
<div class="modal-body">
<p>亲~ 该视频只能试看5s，若需完整观看，请付费！</p>
</div>
<div class="modal-footer">
<button class="btn" data-dismiss="modal" aria-hidden="true">Cancle</button>
<button class="btn btn-primary">Go To Pay</button>
</div>
</div>

<script src="http://twitter.github.com/bootstrap/assets/js/bootstrap-transition.js"></script>
<script src="http://twitter.github.com/bootstrap/assets/js/bootstrap-alert.js"></script>
<script src="http://twitter.github.com/bootstrap/assets/js/bootstrap-modal.js"></script>
<script src="http://twitter.github.com/bootstrap/assets/js/bootstrap-dropdown.js"></script>
<script src="http://twitter.github.com/bootstrap/assets/js/bootstrap-scrollspy.js"></script>
<script src="http://twitter.github.com/bootstrap/assets/js/bootstrap-tab.js"></script>
<script src="http://twitter.github.com/bootstrap/assets/js/bootstrap-tooltip.js"></script>
<script src="http://twitter.github.com/bootstrap/assets/js/bootstrap-popover.js"></script>
<script src="http://twitter.github.com/bootstrap/assets/js/bootstrap-button.js"></script>
<script src="http://twitter.github.com/bootstrap/assets/js/bootstrap-collapse.js"></script>
<script src="http://twitter.github.com/bootstrap/assets/js/bootstrap-carousel.js"></script>
<script src="http://twitter.github.com/bootstrap/assets/js/bootstrap-typeahead.js"></script>
<script src="http://twitter.github.com/bootstrap/assets/js/bootstrap-affix.js"></script>
