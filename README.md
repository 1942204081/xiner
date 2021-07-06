<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html>
<head>
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
	<title>给可可爱爱的馨儿</title>
	<script type="text/javascript" src="js/jquery.min.js"></script>
	<script type="text/javascript" src="js/jscex.min.js"></script>
	<script type="text/javascript" src="js/jscex-parser.js"></script>
	<script type="text/javascript" src="js/jscex-jit.js"></script>
	<script type="text/javascript" src="js/jscex-builderbase.min.js"></script>
	<script type="text/javascript" src="js/jscex-async.min.js"></script>
	<script type="text/javascript" src="js/jscex-async-powerpack.min.js"></script>
	<script type="text/javascript" src="js/functions.js" charset="utf-8"></script>
	<script type="text/javascript" src="js/love.js" charset="utf-8"></script>
　　<link rel="shortcut icon" href="images/love.ico"/>
	<link rel="bookmark" href="/mages/love.ico"/>
    <style type="text/css">
		body{margin:0;padding:0;background:#ffe;font-size:14px;font-family:'微软雅黑','宋体',sans-serif;color:#231F20;overflow:auto}
		a{color:#000;font-size:14px;}
		#main{width:100%;}
		#wrap{position:relative;margin:0 auto;width:1100px;height:680px;margin-top:10px;}
		#text{width:400px;height:425px;left:60px;top:80px;position:absolute;}
		#code{display:none;font-size:16px;}
		#clock-box{position:absolute;left:60px;top:550px;font-size:28px;display:none;}
		#clock-box a{font-size:28px;text-decoration:none;}
		#clock{margin-left:48px;}
		#clock .digit{font-size:64px;}
		#canvas{margin:0 auto;width:1100px;height:680px;}
		#error{margin:0 auto;text-align:center;margin-top:60px;display:none;}
		.hand{cursor:pointer;}
		.say{margin-left:5px;}
		.space{margin-right:150px;}
	</style>
</head>
<body>
	<audio id="bgm" src="raw/love.mp3" type="audio/mpeg" loop="loop">无法加载BGM</audio>
	<div id="main">
		<div id="wrap">
			<div id="text">
				<div id="code">
					<font color="#FF0000">
						<span class="say">一生有你的陪伴</span><br>
						<span class="say">便是最幸运的事</span><br>
						<span class="say">遇见你</span><br>
						<span class="say">这辈子从没想过要放弃你</span><br>
						<span class="say">我只要你陪我一起走过剩下日子</span><br>
						<span class="say">星星会说话</span><br>
						<span class="say">石头会开花</span><br>
						<span class="say">穿过夏天的栅栏和冬天的风雪过后</span><br>
						<span class="say">你终会抵达</span><br>
						<span class="say">如果全世界都对你恶意相加</span><br>
						<span class="say">我就对你说上一世情话</span><br>
					</font>
				</div>
			</div>
			<div id="clock-box">
				<span><font color="#666666">小可爱，我们相识已经是</font></span>
				<div id="clock"></div>
			</div>
			<canvas id="canvas" width="1100" height="680"></canvas>
		</div>
	</div>
	<script>
	// 以上内容不要修改


	// 2016 是 年
	var year = 2021;
	// 2 是 月
    var month = 4;
    // 2 是 日
    var day = 21;
    // 这是小时
    var hour = 12;
    // 这是分钟
    var minute = 36;
    // 这是秒
    var second = 0;

    // 以下内容不要修改
    var auto_load = true;
    var auto_load_delay = 1000;
	(
	function() {
    var canvas = $('#canvas');
	var bgm = document.getElementById('bgm');
    var width = canvas.width();
    var height = canvas.height();
    canvas.attr("width", width);
    canvas.attr("height", height);
    var opts = {
        seed: {
            x: width / 2 - 20,
            color: "rgb(190, 26, 37)",
            scale: 2
        },
        branch: [[535, 680, 570, 250, 500, 200, 30, 100, [[540, 500, 455, 417, 340, 400, 13, 100, [[450, 435, 434, 430, 394, 395, 2, 40]]], [550, 445, 600, 356, 680, 345, 12, 100, [[578, 400, 648, 409, 661, 426, 3, 80]]], [539, 281, 537, 248, 534, 217, 3, 40], [546, 397, 413, 247, 328, 244, 9, 80, [[427, 286, 383, 253, 371, 205, 2, 40], [498, 345, 435, 315, 395, 330, 4, 60]]], [546, 357, 608, 252, 678, 221, 6, 100, [[590, 293, 646, 277, 648, 271, 2, 80]]]]]],
        bloom: {
            num: 700,
            width: 1080,
            height: 650,
        },
        footer: {
            width: 1200,
            height: 5,
            speed: 10,
        }
    };
    var tree = new Tree(canvas[0], width, height, opts);
    var seed = tree.seed;
    var foot = tree.footer;
    var hold = 1;
 
    canvas.click(function(e) {
        var offset = canvas.offset(),
        x,
        y;
        x = e.pageX - offset.left;
        y = e.pageY - offset.top;
        if (seed.hover(x, y)) {
            hold = 0;
            canvas.unbind("click");
            canvas.unbind("mousemove");
            canvas.removeClass('hand');
			bgm.play();
        }
    }).mousemove(function(e) {
        var offset = canvas.offset(),
        x,
        y;
        x = e.pageX - offset.left;
        y = e.pageY - offset.top;
        canvas.toggleClass('hand', seed.hover(x, y));
    });
    var seedAnimate = eval(Jscex.compile("async",
    function() {
        seed.draw();
        if(auto_load){
            hold = 0;
        }
        while (hold) {
            $await(Jscex.Async.sleep(10));
        }
        while (seed.canScale()) {
            seed.scale(0.95);
            $await(Jscex.Async.sleep(10));
        }
        while (seed.canMove()) {
            seed.move(0, 2);
            foot.draw();
            $await(Jscex.Async.sleep(10));
        }
    }));
    var growAnimate = eval(Jscex.compile("async",
    function() {
        do {
            tree.grow();
            $await(Jscex.Async.sleep(10));
        } while ( tree . canGrow ());
    }));
    var flowAnimate = eval(Jscex.compile("async",
    function() {
        do {
            tree.flower(2);
            $await(Jscex.Async.sleep(10));
        } while ( tree . canFlower ());
    }));
    var moveAnimate = eval(Jscex.compile("async",
    function() {
        tree.snapshot("p1", 240, 0, 610, 680);
        while (tree.move("p1", 500, 0)) {
            foot.draw();
            $await(Jscex.Async.sleep(10));
        }
        foot.draw();
        tree.snapshot("p2", 500, 0, 610, 680);
        canvas.parent().css("background", "url(" + tree.toDataURL('image/png') + ")");
        canvas.css("background", "#ffe");
        $await(Jscex.Async.sleep(300));
        canvas.css("background", "none");
    }));
    var jumpAnimate = eval(Jscex.compile("async",
    function() {
        var ctx = tree.ctx;
        while (true) {
            tree.ctx.clearRect(0, 0, width, height);
            tree.jump();
            foot.draw();
            $await(Jscex.Async.sleep(25));
        }
    }));
    var textAnimate = eval(Jscex.compile("async",
    function() {
        var together = new Date();
        together.setFullYear(year, (month - 1), (day - 1));
        together.setHours(hour);
        together.setMinutes(minute);
        together.setSeconds(second);
        together.setMilliseconds(0);
        $("#code").show().typewriter();
        $("#clock-box").fadeIn(500);
        while (true) {
            timeElapse(together);
            $await(Jscex.Async.sleep(1000));
        }
    }));
	document.addEventListener('DOMContentLoaded', function () {
	  function audioAutoPlay() {
		  bgm.play();
		  document.addEventListener("WeixinJSBridgeReady", function () {
			  bgm.play();
		  }, false);
	  }
	  audioAutoPlay();
	 });
    var runAsync = eval(Jscex.compile("async",
    function() {
        $await(seedAnimate());
        $await(growAnimate());
        $await(flowAnimate());
        $await(moveAnimate());
        textAnimate().start();
        $await(jumpAnimate());
    }));
    runAsync().start();
})();
	</script>
</body>
</html>
<!DOCTYPE html>
<!DOCTYPE html>




<html lang="en">
<head>
<meta charset="UTF-8">
<title>3D立体</title>
<style type="text/css">
	@charset "utf-8";
	*{
		margin:0;
		padding:0;
	}
	body{
		max-width: 100%;
		min-width: 100%;
		height: 100%;
		background-size: cover;
		background-repeat: no-repeat;
		background-attachment: fixed;
		background-size:100% 100%;
		position: absolute;
		margin-left: auto;
		margin-right: auto;
	}
	li{
		list-style: none;
	}
	.box{
		width:200px;
		height:200px;
		background-size: cover;
		background-repeat: no-repeat;
		background-attachment: fixed;
		background-size:100% 100%;
		position: absolute;
		margin-left: 42%;
		margin-top: 22%;
		-webkit-transform-style:preserve-3d;
		-webkit-transform:rotateX(13deg);
		-webkit-animation:move 5s linear infinite;
	}
	.minbox{
		width:100px;
		height:100px;
		position: absolute;
		left:50px;
		top:30px;
		-webkit-transform-style:preserve-3d;
	}
	.minbox li{
		width:100px;
		height:100px;
		position: absolute;
		left:0;
		top:0;
	}
	.minbox li:nth-child(1){
		background: url(../img/01.png) no-repeat 0 0;
		-webkit-transform:translateZ(50px);
	}
	.minbox li:nth-child(2){
		background: url(../img/02.png) no-repeat 0 0;
		-webkit-transform:rotateX(180deg) translateZ(50px);
	}
	.minbox li:nth-child(3){
		background: url(../img/03.png) no-repeat 0 0;
		-webkit-transform:rotateX(-90deg) translateZ(50px);
	}
	.minbox li:nth-child(4){
		background: url(../img/04.png) no-repeat 0 0;
		-webkit-transform:rotateX(90deg) translateZ(50px);
	}
	.minbox li:nth-child(5){
		background: url(../img/05.png) no-repeat 0 0;
		-webkit-transform:rotateY(-90deg) translateZ(50px);
	}
	.minbox li:nth-child(6){
		background: url(../img/06.png) no-repeat 0 0;
		-webkit-transform:rotateY(90deg) translateZ(50px);
	}
	.maxbox li:nth-child(1){
		background: url(../img/1.png) no-repeat 0 0;
		-webkit-transform:translateZ(50px);
	}
	.maxbox li:nth-child(2){
		background: url(../img/2.png) no-repeat 0 0;
		-webkit-transform:translateZ(50px);
	}
	.maxbox li:nth-child(3){
		background: url(../img/3.png) no-repeat 0 0;
		-webkit-transform:rotateX(-90deg) translateZ(50px);
	}
	.maxbox li:nth-child(4){
		background: url(../img/4.png) no-repeat 0 0;
		-webkit-transform:rotateX(90deg) translateZ(50px);
	}
	.maxbox li:nth-child(5){
		background: url(../img/5.png) no-repeat 0 0;
		-webkit-transform:rotateY(-90deg) translateZ(50px);
	}
	.maxbox li:nth-child(6){
		background: url(../img/6.png) no-repeat 0 0;
		-webkit-transform:rotateY(90deg) translateZ(50px);
	}
	.maxbox{
		width: 800px;
		height: 400px;
		position: absolute;
		left: 0;
		top: -20px;
		-webkit-transform-style: preserve-3d;
		
	}
	.maxbox li{
		width: 200px;
		height: 200px;
		background: #fff;
		border:1px solid #ccc;
		position: absolute;
		left: 0;
		top: 0;
		opacity: 0.2;
		-webkit-transition:all 1s ease;
	}
	.maxbox li:nth-child(1){
		-webkit-transform:translateZ(100px);
	}
	.maxbox li:nth-child(2){
		-webkit-transform:rotateX(180deg) translateZ(100px);
	}
	.maxbox li:nth-child(3){
		-webkit-transform:rotateX(-90deg) translateZ(100px);
	}
	.maxbox li:nth-child(4){
		-webkit-transform:rotateX(90deg) translateZ(100px);
	}
	.maxbox li:nth-child(5){
		-webkit-transform:rotateY(-90deg) translateZ(100px);
	}
	.maxbox li:nth-child(6){
		-webkit-transform:rotateY(90deg) translateZ(100px);
	}
	.box:hover ol li:nth-child(1){
		-webkit-transform:translateZ(300px);
		width: 400px;
		height: 400px;
		opacity: 0.8;
		left: -100px;
		top: -100px;
	}
	.box:hover ol li:nth-child(2){
		-webkit-transform:rotateX(180deg) translateZ(300px);
		width: 400px;
		height: 400px;
		opacity: 0.8;
		left: -100px;
		top: -100px;
	}
	.box:hover ol li:nth-child(3){
		-webkit-transform:rotateX(-90deg) translateZ(300px);
		width: 400px;
		height: 400px;
		opacity: 0.8;
		left: -100px;
		top: -100px;
	}
	.box:hover ol li:nth-child(4){
		-webkit-transform:rotateX(90deg) translateZ(300px);
		width: 400px;
		height: 400px;
		opacity: 0.8;
		left: -100px;
		top: -100px;
	}
	.box:hover ol li:nth-child(5){
		-webkit-transform:rotateY(-90deg) translateZ(300px);
		width: 400px;
		height: 400px;
		opacity: 0.8;
		left: -100px;
		top: -100px;
	}
	.box:hover ol li:nth-child(6){
		-webkit-transform:rotateY(90deg) translateZ(300px);
		width: 400px;
		height: 400px;
		opacity: 0.8;
		left: -100px;
		top: -100px;
	}
	@keyframes move{
		0%{
			-webkit-transform: rotateX(13deg) rotateY(0deg);
		}
		100%{
			-webkit-transform:rotateX(13deg) rotateY(360deg);
		}
	}
</style>
</head>
<body>
<div class="box">
	<ul class="minbox">
		<li></li>
		<li></li>
		<li></li>
		<li></li>
		<li></li>
		<li></li>
	</ul>
	<ol class="maxbox">
		<li></li>
		<li></li>
		<li></li>
		<li></li>
		<li></li>
		<li></li>
	</ol>
</div>
</body>
</html>
