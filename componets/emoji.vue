<template>
	<view style="width: 100%; height: 100%">
		<u-transition mode="fade" :show="!show" style="width: 100%; height: 100%; display: flex; align-items: center; justify-content: center; font-size: 8vh; color: aqua">
			<div class="loading-container">
				<!-- 环形Loading -->
				<div class="magic-loading"></div>
				<!-- 加载提示文字 -->
				<div class="loading-text">加载中...</div>
			</div>
		</u-transition>
		<u-transition
			mode="fade"
			style="width: 100%; height: 100%; overflow-y: auto; padding-top: 10vh; padding-bottom: 10vh; display: flex; flex-direction: column; align-items: center"
			:show="show"
		>
			<view
				style="
					font-family: 'Orbitron', sans-serif;
					font-size: 4vh;
					font-weight: 800;
					margin-bottom: 2vh;
					margin-top: 0vh;
					color: #3c9cff;
					text-shadow: 0 0 10px rgba(60, 156, 255, 0.3);
				"
			>
				{{ '素材合集' }}
			</view>
			<view
				style="
					width: 80vw;
					display: flex;
					flex-direction: row;
					align-items: center;
					background-color: rgba(255, 255, 255, 0.5);
					padding: 1vh;
					font-size: 2vh;
					justify-content: space-around;
					margin-top: 2vh;
					flex-wrap: wrap;
					padding-top: 2vh;
					padding-bottom: 2vh;
				"
			>
				<liu-waterfall :dataList="emojilist" :column="10" style="width: 80vw" @click="click"></liu-waterfall>
				<view style="width: 100%; height: 10vh"></view>
			</view>
		</u-transition>
	</view>
</template>

<script>
export default {
	data() {
		return {
			emojilist: [],
			show: false,
		}
	},
	methods: {
		click(e) {
			window.open('https://image.begonia.cafe/tx/emoji/' + e.picUrl)
		},
	},
	mounted() {
		uni.request({
			url: '/api/getemojilist',
			method: 'POST',
			data: {},
			success: (res) => {
				for (var x = 0; x < res.data.data.length; x++) {
					this.emojilist.push({
						picUrl: res.data.data[x],
						id: x + 1,
					})
				}
				this.show = true
			},
		})
	},
}
</script>

<style>
/* 基础容器：居中定位 */
.loading-container {
	position: fixed;
	top: 0;
	left: 0;
	width: 100vw;
	height: 100vh;
	background-color: rgba(255, 255, 255, 0.8);
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	z-index: 9999; /* 确保在最上层 */
}

/* 核心Loading环形 */
.magic-loading {
	width: 80px; /* 环形大小 */
	height: 80px;
	border-radius: 50%; /* 圆形 */
	/* 渐变边框：魔幻青+紫色，模拟科技感 */
	border: 6px solid transparent;
	border-top-color: #5de6dc; /* 主题青色 */
	border-right-color: #a78bfa; /* 辅助紫色 */
	border-bottom-color: #5de6dc;
	border-left-color: #a78bfa;
	/* 旋转动画：匀速、无限循环 */
	animation: loadingRotate 1.2s linear infinite;
	position: relative;
}

/* 环形内部小光点（增强细节） */
.magic-loading::after {
	content: '';
	position: absolute;
	top: 8px;
	right: 8px;
	width: 12px;
	height: 12px;
	border-radius: 50%;
	background-color: #5de6dc;
	box-shadow: 0 0 10px rgba(93, 230, 220, 0.8); /* 发光效果 */
}

/* 加载文字提示 */
.loading-text {
	margin-top: 20px;
	font-size: 18px;
	color: #3bc8be; /* 深色主题青 */
	text-shadow: 0 0 5px rgba(93, 230, 220, 0.5);
	/* 文字呼吸效果 */
	animation: loadingFade 2s ease-in-out infinite alternate;
}

/* 旋转动画定义 */
@keyframes loadingRotate {
	from {
		transform: rotate(0deg);
	}
	to {
		transform: rotate(360deg);
	}
}

/* 文字呼吸动画定义 */
@keyframes loadingFade {
	from {
		opacity: 0.7;
		transform: scale(1);
	}
	to {
		opacity: 1;
		transform: scale(1.05);
	}
}
</style>
