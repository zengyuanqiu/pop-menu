<template>
	<!-- 下拉组件  -->
	<div id="popup-menu">
		<div class="btn" ref='btn' style='display:inline-block;padding:0 3px;'>
			<slot></slot>
		</div>
		<div class="mask" ref='mask' @click='hideMenu' v-show='isShow'></div>
		<div v-show='isShow' class="menu" ref='menu' :style='"background:"+bgColor+";"'>
			<span class="arrow" ref='arrow'></span>
			<slot name='menu'></slot>
		</div>
	</div>
</template>

<script type='text/ecmascript-6'>
	export default {
		data() {
			return {
				
			}
		},
		
		props: {
			isShow: {
				type: Boolean,
				default: false
			},
			
			bgColor: {
				type: String,
				default: '#fff'
			}
		},
		
		created() {
			
		},
		
		methods: {
			hideMenu() {
				this.$emit('changeShowVal')
			}
		},
		
		mounted() {
			var btn = this.$refs.btn,
				menu = this.$refs.menu,
				arrow = this.$refs.arrow,
				top = btn.offsetTop,
				left = btn.offsetLeft,
				right = btn.offsetLeft + btn.offsetWidth,
				bottom = btn.offsetTop + btn.offsetHeight,
				centerY = window.innerHeight / 2,
				centerX = window.innerWidth / 2,
				posBtnCenter = Math.max(btn.offsetWidth / 2 - 6, 0);
				
			if(centerY - bottom > 0) { 
				menu.style.top = bottom + 6 + 'px';
				arrow.style.cssText = `top:-5px;
					border-bottom-color:${this.bgColor};
					border-top-width:0;`
			}else {
				menu.style.bottom = centerY * 2 - top + 6 + 'px';
				arrow.style.cssText = `bottom:-5px;
					border-top-color:${this.bgColor};
					border-bottom-width:0;`
			}
			
			
			centerX - left > 0
				? (function() {
					menu.style.left = left + 'px'
					arrow.style.cssText += `left:${posBtnCenter}px;`
				})()
				: (function() {
					menu.style.right = centerX * 2 - right + 'px'
					arrow.style.cssText += `right:${posBtnCenter}px;`
				})();
				
			document.body.appendChild(this.$refs.mask)
			document.body.appendChild(this.$refs.menu)
			
		},
		
		components: {}
	}
</script>

<style scoped lang='less' rel='stylesheet/less'>
	.menu{
		position: fixed;
		z-index: 1000;
		.arrow{
			position: absolute;
			border-color: transparent;
			border-style: solid;
			border-width: 6px;
		}
	}
	.mask{
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		z-index: 999;
	}
</style>
