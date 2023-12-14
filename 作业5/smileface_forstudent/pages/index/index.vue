<!-- 本案例为笑脸的素材 
运行时通过修改机型来观察运行结果
考察：uni-app中的尺寸单位，Canvas，绘图API：uni.canvasToTempFilePath，
以及CanvasContext的相关操作。
对应的，smileface项目的CanvasInRpx.vue为完成版本
-->
<template>
	<view>
		<view>
			<canvas canvas-id="mycanvas" class="mycanvas" @error="canvasErrorHandler"></canvas>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				edge
			}
		},
		onReady: function(e) {
			this.edge=wx.getSystemInfoSync().windowWidth/375;
			const context = uni.createCanvasContext('mycanvas');
			context.scale(this.edge,this.edge);
			context.setStrokeStyle("#00ff00");
			context.setLineWidth(5);
			context.rect(0, 0, 200, 200);
			context.stroke();

			context.setStrokeStyle("#ff0000")
			context.setLineWidth(2)
			context.moveTo(160, 100)
			context.arc(100, 100, 60, 0, 2 * Math.PI, true)
			context.moveTo(140, 100)
			context.arc(100, 100, 40, 0, Math.PI, false)
			context.moveTo(85, 80)
			context.arc(80, 80, 5, 0, 2 * Math.PI, true)
			context.moveTo(125, 80)
			context.arc(120, 80, 5, 0, 2 * Math.PI, true)

			context.stroke()
			context.draw()

			uni.canvasToTempFilePath({
				x: 0,
				y: 0,
				width: 200,
				height: 200,
				destWidth: 400,
				destHeight: 400,
				canvasId: 'mycanvas',
			 success: function(res) {
					console.log("tempFilePath : " + res.tempFilePath)
				}
			})
		},
		methods: {
			canvasErrorHandler: function(e) {
				console.error(e.detail.errMsg)
			}
		}
	}
</script>

<style>
	.mycanvas {
		width: 400rpx;
		height: 400rpx;
		background: orange;
		margin: 100rpx auto;
	}
</style>
