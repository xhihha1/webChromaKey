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

`index.html`  

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
	
`main.js`	

	var processor = {
	  timerCallback: function() {
		if (this.video.paused || this.video.ended) {
		  return;
		}
		this.computeFrame();
		let self = this;
		setTimeout(function () {
			self.timerCallback();
		  }, 0);
	  },

	  doLoad: function() {
		  console.log('go')
		this.video = document.getElementById("video");
		this.c1 = document.getElementById("c1");
		this.ctx1 = this.c1.getContext("2d");
		this.c2 = document.getElementById("c2");
		this.ctx2 = this.c2.getContext("2d");
		let self = this;
		this.video.addEventListener("play", function() {
			self.width = self.video.videoWidth / 2;
			self.height = self.video.videoHeight / 2;
			self.timerCallback();
		  }, false);
	  },

	  computeFrame: function() {
		this.ctx1.drawImage(this.video, 0, 0, this.width, this.height);
		let frame = this.ctx1.getImageData(0, 0, this.width, this.height);
			let l = frame.data.length / 4;

		for (let i = 0; i < l; i++) {
		  let r = frame.data[i * 4 + 0];
		  let g = frame.data[i * 4 + 1];
		  let b = frame.data[i * 4 + 2];
		  if (g > 100 && r > 100 && b < 43)
			frame.data[i * 4 + 3] = 0;
		}
		this.ctx2.putImageData(frame, 0, 0);
		return;
	  }
	};

