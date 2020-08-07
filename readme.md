# 色鍵，綠幕

[Wiki介紹](https://zh.wikipedia.org/wiki/%E8%89%B2%E9%94%AE)  
[原始參考MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API/Manipulating_video_using_canvas)


![demo](readme/demo.png)  
[Demo 運行代碼](https://xhihha1.github.io/webChromaKey/)

- index.html  
- ./script/main.js  
- ./script/foo.png  
- ./script/video.ogv  

原始參考網站內容如果直接使用是無法執行，需要進行修改。
主要修改是 `<script />` 改為 `<script></script>`  
同理 `<canvas />` 改為 `<canvas></canvas>`

	<html>
	  <head>
		<style>
		  body {
			background: black;
			color:#CCCCCC; 
		  }
		  #c2 {
			background-image: url(./script/foo.png);
			background-repeat: no-repeat;
		  }
		  div {
			float: left;
			border :1px solid #444444;
			padding:10px;
			margin: 10px;
			background:#3B3B3B;
		  }
		</style>
		<script>
			console.log('go1')
		</script>
		<script src="./script/main.js"></script>
	  </head>

	  <body onload="processor.doLoad()" cz-shortcut-listen="true">
		<div>
		  <video id="video" src="./script/video.ogv" controls="true" />
		</div>
		<div>
		  <canvas id="c1" width="160" height="96" ></canvas>
		  <canvas id="c2" width="160" height="96" ></canvas>
		</div>
	  </body>
	</html>