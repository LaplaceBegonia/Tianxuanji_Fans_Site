<template>
	<view style="width: 100vw; height: 100vh; overflow-y: auto; padding-top: 10vh; padding-bottom: 10vh; overflow-x: hidden">
		<u-transition show>
			<view
				style="width: 40vw; margin-left: 30vw; height: auto; background-color: rgba(255, 255, 255, 0.6); box-shadow: 0 0 5px #3c9cff; border-radius: 10px; font-size: 2.2vh"
			>
				<view style="display: flex; flex-direction: column; align-items: center; justify-content: space-around; color: #3489dd">
					<view style="display: flex; flex-direction: row; align-items: center; justify-content: center" @click="click('https://space.bilibili.com/703405')">
						<image src="/static/tx.png" style="height: 9vh; margin-left: 2vw; margin-right: 2vw; margin-top: 1vw; margin-bottom: 1vw" mode="heightFix"></image>
						<text>天选姬_Official的哔哩哔哩主页</text>
					</view>
					<view style="display: flex; flex-direction: row; align-items: center; justify-content: center" @click="click('https://space.bilibili.com/3494357252442916')">
						<image src="/static/rog.png" style="height: 9vh" mode="heightFix"></image>
						<text>RO姬_Official的哔哩哔哩主页</text>
					</view>
					<view style="display: flex; flex-direction: row; align-items: center; justify-content: center" @click="click('https://space.bilibili.com/1639389144')">
						<image src="/static/_ELEVEN.png" style="height: 3.5vh; margin: 1vw" mode="heightFix"></image>
						<text>ElevenOfficial_的哔哩哔哩主页</text>
					</view>
				</view>
				<!-- 插入分割线 -->
				<hr class="module-divider" />
				<view style="display: flex; width: 100%; align-items: center; justify-content: center; margin-bottom: 0vh">
					<image src="/static/bilibili.png" style="height: 8vh" mode="heightFix"></image>
				</view>
				<view
					style="display: flex; flex-direction: row; align-items: center; justify-content: space-around; color: #ff557f; margin-bottom: 2vh"
					@click="click('https://space.bilibili.com/471130755')"
				>
					<text>华硕天选官方UP的哔哩哔哩主页</text>
				</view>
				<!-- 插入分割线 -->
				<hr class="live-divider" />

				<view style="display: flex; flex-direction: row; align-items: center; justify-content: space-around; color: #ff557f">
					<view
						style="display: flex; flex-direction: column; width: 33%; align-items: center; justify-content: center"
						@click="click('https://live.bilibili.com/2058234')"
					>
						<image src="/static/bilibililive.png" style="height: 3vh; margin-bottom: 2vh" mode="heightFix"></image>
						<text>天选姬_Official的直播间</text>
					</view>
					<view
						style="display: flex; flex-direction: column; width: 33%; align-items: center; justify-content: center"
						@click="click('https://live.bilibili.com/30326232')"
					>
						<image src="/static/bilibililive.png" style="height: 3vh; margin-bottom: 2vh" mode="heightFix"></image>
						<text>RO姬_Official的直播间</text>
					</view>
					<view
						style="display: flex; flex-direction: column; width: 33%; align-items: center; justify-content: center"
						@click="click('https://live.bilibili.com/25896305')"
					>
						<image src="/static/bilibililive.png" style="height: 3vh; margin-bottom: 2vh" mode="heightFix"></image>
						<text>ElevenOfficial_的直播间</text>
					</view>
				</view>
				<!-- 插入跨平台分割线 -->
				<hr class="live-divider" />
				<view style="display: flex; flex-direction: row; align-items: center; justify-content: center">
					<view style="display: flex; flex-direction: column; align-items: center; justify-content: center; width: 33%">
						<view
							style="display: flex; width: 100%; align-items: center; justify-content: center; margin-top: 2vh; margin-bottom: 1vh"
							@click="click('https://www.douyin.com/user/MS4wLjABAAAAk7Y4ViKdZ1DtpUoKQpK7OiyNePkhXfZt60VKHipeUyg')"
						>
							<image src="/static/douyin.png" style="height: 5vh" mode="heightFix"></image>
						</view>
						<view
							style="display: flex; flex-direction: row; align-items: center; justify-content: space-around; color: #8b5cf6; margin-bottom: 2vh"
							@click="click('https://www.douyin.com/user/MS4wLjABAAAAk7Y4ViKdZ1DtpUoKQpK7OiyNePkhXfZt60VKHipeUyg')"
						>
							<text>天选姬抖音主页</text>
						</view>
					</view>
					<view style="display: flex; flex-direction: column; align-items: center; justify-content: center; width: 33%">
						<view
							style="display: flex; width: 100%; align-items: center; justify-content: center; margin-top: 2vh; margin-bottom: 1vh"
							@click="click('https://www.xiaohongshu.com/user/profile/6184b692000000001000515e')"
						>
							<image src="/static/xhs.png" style="height: 4vh" mode="heightFix"></image>
						</view>
						<view
							style="display: flex; flex-direction: row; align-items: center; justify-content: space-around; color: #ff4141; margin-bottom: 2vh"
							@click="click('https://www.xiaohongshu.com/user/profile/6184b692000000001000515e')"
						>
							<text>天选姬小红书主页</text>
						</view>
					</view>

					<view style="display: flex; flex-direction: column; align-items: center; justify-content: center; width: 33%">
						<view
							style="display: flex; width: 100%; align-items: center; justify-content: center; margin-top: 2vh; margin-bottom: 1vh"
							@click="click('https://weibo.com/u/7356387136')"
						>
							<image src="/static/weibo.png" style="height: 4.5vh" mode="heightFix"></image>
						</view>
						<view
							style="display: flex; flex-direction: row; align-items: center; justify-content: space-around; color: #ffaa7f; margin-bottom: 2vh"
							@click="click('https://weibo.com/u/7356387136')"
						>
							<text>天选姬官方微博</text>
						</view>
					</view>
				</view>
				<!-- 插入跨平台分割线 -->
				<hr class="platform-divider" />
				<view style="display: flex; flex-direction: row; align-items: center; justify-content: center">
					<view style="display: flex; flex-direction: column; align-items: center; justify-content: center; width: 33%">
						<view
							style="display: flex; width: 100%; align-items: center; justify-content: center; margin-top: 2vh; margin-bottom: 1vh"
							@click="click('https://zh.moegirl.org.cn/%E5%A4%A9%E9%80%89%E5%A7%AC')"
						>
							<image src="/static/mnbk.svg" style="height: 4.5vh" mode="heightFix"></image>
						</view>
						<view
							style="display: flex; flex-direction: row; align-items: center; justify-content: space-around; color: #0055ff; margin-bottom: 2vh"
							@click="click('https://zh.moegirl.org.cn/%E5%A4%A9%E9%80%89%E5%A7%AC')"
						>
							<text>天选姬的萌娘百科</text>
						</view>
					</view>
					<view style="display: flex; flex-direction: column; align-items: center; justify-content: center; width: 33%">
						<view
							style="display: flex; width: 100%; align-items: center; justify-content: center; margin-top: 2vh; margin-bottom: 1vh"
							@click="click('https://zh.moegirl.org.cn/RO姬')"
						>
							<image src="/static/mnbk.svg" style="height: 4.5vh" mode="heightFix"></image>
						</view>
						<view
							style="display: flex; flex-direction: row; align-items: center; justify-content: space-around; color: #0055ff; margin-bottom: 2vh"
							@click="click('https://zh.moegirl.org.cn/RO姬')"
						>
							<text>RO姬的萌娘百科</text>
						</view>
					</view>
				</view>
				<!-- 插入跨平台分割线 -->
				<hr class="module-divider" />
				<view style="display: flex; flex-direction: row; align-items: center; justify-content: center">
					<view style="display: flex; flex-direction: column; align-items: center; justify-content: center; width: 33%">
						<view
							style="height: 7vh; display: flex; width: 100%; align-items: center; justify-content: center; margin-top: 2vh; margin-bottom: 1.5vh"
							@click="click('https://www.asus.com.cn/laptops/for-gaming/tuf-gaming/')"
						>
							<image src="/static/asus.svg" style="height: 4vh" mode="heightFix"></image>
						</view>
						<view
							style="display: flex; flex-direction: row; align-items: center; justify-content: space-around; color: #0041c5; margin-bottom: 2vh"
							@click="click('https://www.asus.com.cn/laptops/for-gaming/tuf-gaming/')"
						>
							<text>华硕天选</text>
						</view>
					</view>
					<view style="display: flex; flex-direction: column; align-items: center; justify-content: center; width: 33%">
						<view
							style="height: 7vh; display: flex; width: 100%; align-items: center; justify-content: center; margin-top: 2vh; margin-bottom: 1.5vh"
							@click="click('https://rog.asus.com.cn/')"
						>
							<image src="/static/ROG1.png" style="height: 7vh" mode="heightFix"></image>
						</view>
						<view
							style="display: flex; flex-direction: row; align-items: center; justify-content: space-around; color: #ff0000; margin-bottom: 2vh"
							@click="click('https://rog.asus.com.cn/')"
						>
							<text>ROG玩家国度</text>
						</view>
					</view>
					<view style="display: flex; flex-direction: column; align-items: center; justify-content: center; width: 33%">
						<view
							style="height: 7vh; display: flex; width: 100%; align-items: center; justify-content: center; margin-top: 2vh; margin-bottom: 1.5vh"
							@click="click('https://event.asus.com.cn/acm/index.html')"
						>
							<image src="/static/acm.png" style="height: 8vh" mode="heightFix"></image>
						</view>
						<view
							style="display: flex; flex-direction: row; align-items: center; justify-content: space-around; color: #ad7300; margin-bottom: 2vh"
							@click="click('https://event.asus.com.cn/acm/index.html')"
						>
							<text>ACM华硕校园合伙人</text>
						</view>
					</view>
				</view>
				<view style="height: 2vh; width: 100vw"></view>
			</view>
			<view style="height: 20vh; width: 100vw"></view>
		</u-transition>
	</view>
</template>

<script>
export default {
	data() {
		return {}
	},
	methods: {
		click(e) {
			window.open(e)
		},
	},
}
</script>

<style>
/* 通用分割线样式：渐变+圆角，契合IP风格 */
.module-divider {
	height: 1px;
	min-height: 4px;
	max-height: 3px;
	margin: 24px 0;
	background: linear-gradient(90deg, transparent, #2563eb, transparent); /* 天选蓝渐变 */
	border: none;
	width: 90%;
	margin-left: 5%;
}

/* 直播间板块分割线：强化B站属性 */
.live-divider {
	height: 1px;
	min-height: 3px;
	max-height: 2px;
	background: linear-gradient(90deg, transparent, #fb7299, transparent); /* B站直播粉渐变 */
	margin: 32px 0;
	width: 90%;
	margin-left: 5%;
	border: none;
}

/* 跨平台板块分割线：多平台融合感 */
.platform-divider {
	height: 1px;
	min-height: 3px;
	max-height: 2px;
	background: linear-gradient(90deg, #00000000, #8b5cf6, #00000000); /* 紫蓝渐变，区分跨平台区域 */
	margin: 28px 0;
	width: 90%;
	margin-left: 5%;
	border: none;
}
</style>
