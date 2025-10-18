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
		<u-transition mode="fade" :show="show" style="width: 100%; height: 100%">
			<view
				style="width: 100%; height: 100%; overflow-y: auto; padding-top: 10vh; padding-bottom: 10vh; display: flex; flex-direction: column; align-items: center"
				v-if="show"
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
					{{ '切片' }}
				</view>
				<view
					style="
						border-radius: 10px 10px 0 0;
						box-shadow: 0 0 15px rgba(193, 229, 255, 0.8);
						width: 77vw;
						display: flex;
						flex-direction: row;
						align-items: center;
						background: linear-gradient(180deg, rgba(255, 255, 255, 0.7), rgba(255, 255, 255, 0.4));
						padding: 1vh 2vw;
						font-size: 2vh;
						justify-content: space-between;
						margin-top: 2vh;
						backdrop-filter: blur(8px);
					"
				>
					<view
						:style="{
							color: sub == 0 ? '#54d1c7' : '#333',
							padding: '1vh 2vw',
							borderRadius: '8px',
							fontWeight: sub == 0 ? 'bold' : 'normal',
							background: sub == 0 ? 'rgba(93, 230, 220, 0.15)' : 'transparent',
							transition: 'all 0.3s ease',
							minWidth: '8vw',
							textAlign: 'center',
							textShadow: sub == 0 ? '0 0 5px rgba(93, 230, 220, 0.6)' : 'none',
						}"
						@click="((sub = 0), getvideolist())"
						hover:style="{
				      background: sub!=0 ? 'rgba(93, 230, 220, 0.08)' : 'rgba(93, 230, 220, 0.15)',
				      transform: 'translateY(-2px)'
				    }"
					>
						{{ '全部' }}
					</view>

					<view
						:style="{
							color: sub == 1 ? '#54d1c7' : '#333',
							padding: '1vh 2vw',
							borderRadius: '8px',
							fontWeight: sub == 1 ? 'bold' : 'normal',
							background: sub == 1 ? 'rgba(93, 230, 220, 0.15)' : 'transparent',
							transition: 'all 0.3s ease',
							minWidth: '8vw',
							textAlign: 'center',
							textShadow: sub == 1 ? '0 0 5px rgba(93, 230, 220, 0.6)' : 'none',
						}"
						@click="((sub = 1), getvideolist())"
						hover:style="{
				      background: sub!=1 ? 'rgba(93, 230, 220, 0.08)' : 'rgba(93, 230, 220, 0.15)',
				      transform: 'translateY(-2px)'
				    }"
					>
						{{ '歌切' }}
					</view>

					<view
						:style="{
							color: sub == 2 ? '#54d1c7' : '#333',
							padding: '1vh 2vw',
							borderRadius: '8px',
							fontWeight: sub == 2 ? 'bold' : 'normal',
							background: sub == 2 ? 'rgba(93, 230, 220, 0.15)' : 'transparent',
							transition: 'all 0.3s ease',
							minWidth: '8vw',
							textAlign: 'center',
							textShadow: sub == 2 ? '0 0 5px rgba(93, 230, 220, 0.6)' : 'none',
						}"
						@click="((sub = 2), getvideolist())"
						hover:style="{
				      background: sub!=2 ? 'rgba(93, 230, 220, 0.08)' : 'rgba(93, 230, 220, 0.15)',
				      transform: 'translateY(-2px)'
				    }"
					>
						{{ '切片' }}
					</view>

					<view
						:style="{
							color: sub == 3 ? '#54d1c7' : '#333',
							padding: '1vh 2vw',
							borderRadius: '8px',
							fontWeight: sub == 3 ? 'bold' : 'normal',
							background: sub == 3 ? 'rgba(93, 230, 220, 0.15)' : 'transparent',
							transition: 'all 0.3s ease',
							minWidth: '8vw',
							textAlign: 'center',
							textShadow: sub == 3 ? '0 0 5px rgba(93, 230, 220, 0.6)' : 'none',
						}"
						@click="((sub = 3), getvideolist())"
						hover:style="{
				      background: sub!=3 ? 'rgba(93, 230, 220, 0.08)' : 'rgba(93, 230, 220, 0.15)',
				      transform: 'translateY(-2px)'
				    }"
					>
						{{ '二创' }}
					</view>

					<view
						:style="{
							color: sub == 4 ? '#5DE6DC' : '#333',
							padding: '1vh 2vw',
							borderRadius: '8px',
							fontWeight: sub == 4 ? 'bold' : 'normal',
							background: sub == 4 ? 'rgba(93, 230, 220, 0.15)' : 'transparent',
							transition: 'all 0.3s ease',
							minWidth: '8vw',
							textAlign: 'center',
							textShadow: sub == 4 ? '0 0 5px rgba(93, 230, 220, 0.6)' : 'none',
						}"
						@click="((sub = 4), getvideolist())"
						hover:style="{
				      background: sub!=4 ? 'rgba(93, 230, 220, 0.08)' : 'rgba(93, 230, 220, 0.15)',
				      transform: 'translateY(-2px)'
				    }"
					>
						{{ '录播' }}
					</view>
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
						box-shadow: 0 0 15px rgba(193, 229, 255, 0.8);
						border-radius: 0 0 10px 10px;
					"
				>
					<view
						style="
							width: 30%;
							height: 130px;
							margin-bottom: 10px;
							display: flex;
							flex-direction: row;
							align-items: center;
							padding: 10px;
							box-shadow: 0px 0px 5px rgba(60, 156, 255, 0.5);
							border-radius: 10px;
							background-color: rgba(255, 255, 255, 0.8);
						"
						v-for="(item, index) in videolist"
						@click="openpage(item.bv)"
						v-if="sub != 4"
					>
						<img
							:src="item.pic"
							style="height: 130px; max-width: 200px; min-width: 200px; border-radius: 5px; margin-right: 15px; object-fit: cover"
							referrerpolicy="no-referrer"
						/>
						<view style="height: 130px; width: 100%; display: flex; flex-direction: column">
							<text style="font-size: 1.1rem">{{ item.title }}</text>
							<u--text size="16" lines="2" color="rgb(96, 98, 102)" :text="item.desc.replaceAll('\n', '')"></u--text>
							<view style="display: flex; flex-direction: row; align-items: center; font-size: 1rem; width: 100%">
								<img
									referrerpolicy="no-referrer"
									:src="item.face"
									style="width: 30px; height: 30px; border-radius: 50%; margin-right: 10px; object-fit: cover"
									mode="aspectFill"
								/>
								<text style="font-size: 1.3vh">{{ item.author }}</text>
								<view style="font-size: 1.3vh; margin-left: auto">{{ '类型:' + (item.type == 1 ? '歌切' : item.type == 2 ? '切片' : '二创') }}</view>
							</view>
						</view>
					</view>
					<view
						style="
							width: 30%;
							height: 130px;
							background-color: rgba(255, 255, 255, 0.8);
							border-radius: 10px;
							margin-bottom: 10px;
							display: flex;
							flex-direction: row;
							align-items: center;
							padding-top: 10px;
							padding-left: 10px;
							padding-bottom: 10px;
							box-shadow: 0px 0px 5px rgba(60, 156, 255, 0.5);
						"
						v-for="(item, index) in history"
						v-if="sub == 4"
					>
						<img
							referrerpolicy="no-referrer"
							:src="item.live_info.cover"
							style="object-fit: cover; height: 130px; max-width: 200px; min-width: 200px; border-radius: 5px; margin-right: 15px"
							mode="aspectFill"
						/>
						<view style="height: 130px; width: 100%; display: flex; flex-direction: column">
							<text style="font-size: 1.1rem" :style="{ color: fontcolor }">{{ item.live_info.title }}</text>
							<text style="font-size: 1.1rem">{{ getdate(item.start_time * 1000) + ' ' + getxingqi(item.start_time * 1000) }}</text>
							<text style="font-size: 1rem">{{ gettime(item.start_time * 1000) + '-' + gettime(item.end_time * 1000) }}</text>
							<view
								style="
									width: 80px;
									display: flex;
									align-items: center;
									justify-content: center;
									border-radius: 5px;
									margin-top: 10px;
									margin-right: auto;
									color: white;
									height: 35px;
									font-size: 1.1rem;
									background-color: #5de6dc;
								"
								@click="
									openpage1(
										'https://live.bilibili.com/web-cut/quick-publish.html?start_time=' +
											item.start_time +
											'&end_time=' +
											item.end_time +
											'&live_key=' +
											item.live_key +
											'&cover=' +
											item.live_info.cover +
											'&anchor_id=' +
											live_uid +
											'&anchor_name=' +
											anchor_name
									)
								"
							>
								<text>{{ '去剪辑' }}</text>
							</view>
						</view>
					</view>
					<view
						style="
							width: 30%;
							height: 130px;
							margin-bottom: 10px;
							display: flex;
							flex-direction: row;
							align-items: center;
							padding-top: 0px;
							padding-bottom: 10px;
							padding: 10px;
						"
						v-if="sub == 4 && 3 - (history.length % 3) != 3"
						v-for="i in 3 - (history.length % 3)"
					></view>
					<view
						style="
							width: 30%;
							height: 130px;
							margin-bottom: 10px;
							display: flex;
							flex-direction: row;
							align-items: center;
							padding-top: 0px;
							padding-bottom: 10px;
							padding: 10px;
						"
						v-if="sub != 4 && 3 - (videolist.length % 3) != 3"
						v-for="i in 3 - (videolist.length % 3)"
					></view>
				</view>
			</view>
		</u-transition>
	</view>
</template>

<script>
export default {
	data() {
		return {
			data: {},
			show: false,
			sub: 0,
			videolist: [],
			live_uid: '703405',
			history: [],
		}
	},
	methods: {
		openpage(e) {
			window.open('https://www.bilibili.com/video/' + e)
		},
		openpage1(e) {
			window.open(e)
		},
		formatDuration(timestamp) {
			// 确保输入是数字类型
			const totalSeconds = parseInt(timestamp)

			// 计算小时、分钟和剩余秒数
			const hours = Math.floor(totalSeconds / 3600)
			const minutes = Math.floor((totalSeconds % 3600) / 60)
			const seconds = totalSeconds % 60

			// 格式化为两位数字符串 (00:00:00)
			const pad = (num) => num.toString().padStart(2, '0')

			return `${pad(hours)}:${pad(minutes)}:${pad(seconds)}`
		},
		getdate(timestamp) {
			const date = new Date(timestamp)
			const year = date.getFullYear()
			const month = String(date.getMonth() + 1).padStart(2, '0') // 月份从0开始
			const day = String(date.getDate()).padStart(2, '0')

			return `${year}-${month}-${day}`
		},
		gettime(timestamp) {
			const date = new Date(timestamp)

			const hours = String(date.getHours()).padStart(2, '0')
			const minutes = String(date.getMinutes()).padStart(2, '0')
			const seconds = String(date.getSeconds()).padStart(2, '0')

			return `${hours}:${minutes}:${seconds}`
		},
		getxingqi(timestamp) {
			const days = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六']
			return days[new Date(timestamp).getDay()]
		},
		getDuration(startDate, stopDate) {
			// 确保输入转换为Date对象
			const start = new Date(startDate)
			const stop = new Date(stopDate)

			// 计算时间差（毫秒）
			const diffMs = stop - start

			// 处理无效日期或结束时间早于开始时间的情况
			if (isNaN(diffMs) || diffMs < 0) {
				return '0h0m'
			}

			// 计算小时和分钟
			const diffMinutes = Math.floor(diffMs / (1000 * 60))
			const hours = Math.floor(diffMinutes / 60)
			const minutes = diffMinutes % 60

			return `${hours}h ${minutes}m`
		},
		getvideolist() {
			if (this.sub == 4) {
				uni.request({
					url: '/api/gethistory',
					method: 'POST',
					data: {
						live_uid: '703405',
					},
					success: (res) => {
						this.history = res.data.data.replay_info
						this.$forceUpdate()
					},
				})
			} else {
				uni.request({
					url: '/api/getvideo',
					method: 'POST',
					data: {
						type: this.sub,
					},
					success: (res) => {
						this.videolist = res.data.data
						this.show = true
						this.$forceUpdate()
					},
				})
			}
		},
	},
	mounted() {
		this.getvideolist()
	},
}
</script>

<style>
.fade-item {
	opacity: 0;
	transition: opacity 0.3s ease-out; /* 淡入过渡效果 */
}

/* 显示状态：透明度为1 */
.fade-item.visible {
	opacity: 1;
}
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
