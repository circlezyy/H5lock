# H5lock
H5九宫格解锁 样式绘图（支持Canvas和图片）

    http://test.go.163.com/go/2016/1227/H5lock/src/H5lock.js

## Demo ##
![qr-code](qr-code/qr-code.png)

[http://test.go.163.com/go/2016/1227/H5lock/](http://test.go.163.com/go/2016/1227/H5lock/)

## 使用 说明 ##

###HTML

	<canvas id="canvas" width="400" height="600"></canvas>

### JavaScript ###

	<script type="text/javascript" src="src/H5lock.js"></script>
	<script type="text/javascript">
        var lock = new H5lock({});
        lock.init(n,m,H5lockImgSrc);//n:列数 m:行数 H5lockImgSrc:图片路径
	</script>

### Option method ###

	lock.reset(); //页面重置

### 示例 ###

    <div id="canvas-box">
    	<a id="updatePassword">重置</a>
    	<canvas id="canvas" width="400" height="600"></canvas>
    </div>  

----------

    <script type="text/javascript" src="src/H5lock.js"></script>
    <script type="text/javascript">
    	// 初始化
    	var lock = new H5lock({});
    	//4列,6行,图片路径
    	lock.init(4,6,"src/star3.png");
    	// 重置按钮
    	document.getElementById('updatePassword').addEventListener('click', function(){
    		lock.reset();
    	});
    </script>

## 高级 ##
H5Lock.js自定义

### 初始页面效果 ###
	H5lock.prototype.drawCle = function(x, y) { // 初始化解锁面板
		// 线条颜色
		this.ctx.strokeStyle = '#CFE6FF';
		// 线条宽度
		this.ctx.lineWidth = 2;
		this.ctx.beginPath();
		this.ctx.arc(x, y, this.r, 0, Math.PI * 2, true);
		this.ctx.closePath();
		this.ctx.stroke();
	}

### 触碰后样式 ###

#### 图片实现 ####
	H5lock.prototype.drawPoint = function() { // 初始化触碰后样式（图片）
		var imgObj = new Image();
		imgObj.src = this.H5lockImgSrc;
		for (var i = 0 ; i < this.lastPoint.length ; i++) {
			var othis = this;
			this.ctx.clearRect(othis.lastPoint[i].x-(othis.r+2), othis.lastPoint[i].y-(othis.r+2), othis.r*2+4, othis.r*2+4);
			this.ctx.drawImage(imgObj,othis.lastPoint[i].x-(othis.r+1), othis.lastPoint[i].y-(othis.r+1), othis.r*2+2, othis.r*2+2);
		}
	}

#### Canvas实现 ####
	H5lock.prototype.drawPoint = function() { // 初始化触碰后样式（Canvas画圆心）
		for (var i = 0 ; i < this.lastPoint.length ; i++) {
			// 填充颜色
			this.ctx.fillStyle = '#CFE6FF';
			this.ctx.beginPath();
			this.ctx.arc(this.lastPoint[i].x, this.lastPoint[i].y, this.r / 2, 0, Math.PI * 2, true);
			this.ctx.closePath();
			this.ctx.fill();
		}
	}

## 补充 ##
 
报错：`Failed to execute 'getImageData' on 'CanvasRenderingContext2D': The canvas has been tainted by cross-origin data.`    
原因：getImageData此方法不允许操作非此域名外的图片资源，即使是子域也不行  
解决办法：  


- 使用本地服务器进行测试
- [--disable-web-security](http://www.bkjia.com/webzh/994015.html)
- [将图片转换成为字符串保存在浏览器，使用时再转换](http://blog.csdn.net/molaifeng/article/details/42293509)


----------

H5解锁密码识别功能：[https://github.com/lvming6816077/H5lock](https://github.com/lvming6816077/H5lock)