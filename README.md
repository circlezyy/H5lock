# H5lock
H5九宫格解锁 样式绘图（支持Canvas和图片）

http://test.go.163.com/go/2016/1227/H5lock/src/H5lock.js

## demo ##
![qr-code](qr-code/qrcode.png)

## 使用说明 ##
H5lock.js

- HTML

	    <canvas id="canvas" width="400" height="600"></canvas>

- JavaScript

		<script type="text/javascript" src="src/H5lock.js"></script>
		<script type="text/javascript">
        	// 初始化
        	var lock = new H5lock({});
        	// lock.init(n,m,H5lockImgSrc) n列,m行
        	lock.init(4,6,"src/star3.png");

        	// 重置按钮
        	document.getElementById('updatePassword').addEventListener('click', function(){
            	lock.reset();
        	});
		</script>