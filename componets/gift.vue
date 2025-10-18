<template>
	<view style="width: 100%; height: 100%; overflow-y: auto">
		<u-transition :show="show" mode="fade" style="width: 100%; height: 100%; display: flex; align-items: center; flex-direction: column">
			<!-- 标题区域 -->
			<div class="title-container" style="height: 6vw; width: 100vw; display: flex; flex-direction: column; align-items: center; justify-content: center">
				<h1 style="font-size: 2vw; margin: 0; padding: 0">🚢 天选姬の大航海回馈列表 ⚓</h1>
				<view style="display: flex; flex-direction: row; align-items: center; justify-content: center; margin-top: 0.5vw">
					<p style="font-size: 1vw; margin: 0">感谢各位舰长/提督/总督的支持！专属福利已激活～</p>
					<image src="/static/emoji.png" style="height: 2.5vw; width: 2.5vw; margin-left: 0.5vw"></image>
				</view>
			</div>

			<!-- 主内容区域 -->
			<view style="height: auto; width: 78vw; margin-top: 1vw; display: flex; flex-direction: column; padding: 1vw">
				<!-- 月度回馈循环 -->
				<view
					v-for="(item, index) in list"
					style="
						box-shadow: 0 0 15px rgba(193, 229, 255, 0.8);
						font-size: 1vw;
						margin-bottom: 5vw;
						padding-bottom: 1vw;
						background-color: white;
						padding: 1vw;
						border-radius: 1vw;
					"
				>
					<!-- 头部：标题 + 舰长数 + 发货状态 -->
					<view style="width: 100%; display: flex; flex-direction: row; align-items: center; padding-left: 1%; padding-right: 1%">
						<view style="display: flex; flex-direction: column; align-items: flex-start">
							<text style="font-size: 1.5vw; font-weight: bold">{{ item.title }}</text>
							<view style="margin-left: 0; font-size: 0.8vw; color: #3c9cff; margin-top: 0.5vw" @click="pre(item.url)">查看礼物图示</view>
						</view>
						<view style="display: flex; flex-direction: column; margin-left: auto; align-items: flex-end; margin-right: 2.5%">
							<view style="display: flex; flex-direction: row; align-items: center; margin-left: auto">
								<view style="font-size: 0.9vw; margin-left: auto; color: black">当前舰长数:</view>
								<view style="margin-left: 0.5vw; font-size: 0.9vw; color: #ff6666">
									{{ item.shipnum }}
								</view>
							</view>
							<view style="margin-left: 1vw; color: #4ce570; font-size: 0.9vw; margin-right: 2.5%" v-if="item.status == 2">已发货</view>
							<view style="margin-left: 1vw; color: #ff9933; font-size: 0.9vw; margin-right: 2.5%" v-if="item.status == 1">待发货</view>
							<view style="margin-left: 1vw; color: #3c9cff; font-size: 0.9vw; margin-right: 2.5%" v-if="item.status == 0">待结算</view>
						</view>
					</view>

					<!-- 舰长/提督/总督礼物卡片 -->
					<view
						style="
							display: flex;
							flex-direction: row;
							align-items: stretch;
							width: 100%;
							font-size: 1vw;
							justify-content: space-around;
							margin-top: 1vw;
							color: #2e2f31;
						"
					>
						<!-- 舰长礼物 -->
						<view
							style="
								width: 28%;
								display: flex;
								flex-direction: column;
								background-color: rgba(157, 208, 255, 0.1);
								padding: 1.5%;
								border-radius: 0.5vw;
								box-shadow: 0 0 0.5vw #c2e0ff;
							"
						>
							<view style="display: flex; flex-direction: row; align-items: center">
								<view
									style="
										height: 2.5vw;
										width: 2.5vw;
										display: flex;
										align-items: center;
										justify-content: center;
										background-color: #3c9cff;
										border-radius: 50%;
										box-shadow: 1px 1px 0.5vw #3c9cff;
										margin-right: 1vw;
									"
								>
									<i class="fa-solid fa-ship" style="color: white"></i>
								</view>
								<text style="font-weight: 700; color: black; font-size: 1.2vw">舰长礼物</text>
							</view>
							<view style="font-size: 0.9vw; margin-top: 1vw" v-html="item.gift1.replaceAll('\n', '<br>')"></view>
						</view>
						<!-- 提督礼物 -->
						<view
							style="
								width: 28%;
								display: flex;
								flex-direction: column;
								background-color: rgba(170, 0, 255, 0.1);
								padding: 1.5%;
								border-radius: 0.5vw;
								box-shadow: 0 0 0.5vw #f49dff;
							"
						>
							<view style="display: flex; flex-direction: row; align-items: center">
								<view
									style="
										height: 2.5vw;
										width: 2.5vw;
										display: flex;
										align-items: center;
										justify-content: center;
										background-color: #aa00ff;
										border-radius: 50%;
										box-shadow: 1px 1px 0.5vw #aa00ff;
										margin-right: 1vw;
									"
								>
									<i class="fa-solid fa-anchor" style="color: white"></i>
								</view>
								<text style="font-weight: 700; color: black; font-size: 1.2vw">提督礼物</text>
							</view>
							<view style="font-size: 0.9vw; margin-top: 1vw" v-html="item.gift2.replaceAll('\n', '<br>')"></view>
						</view>
						<!-- 总督礼物 -->
						<view
							style="
								width: 28%;
								display: flex;
								flex-direction: column;
								background-color: rgba(255, 0, 0, 0.1);
								padding: 1.5%;
								border-radius: 0.5vw;
								box-shadow: 0 0 0.5vw #ff8f8f;
							"
						>
							<view style="display: flex; flex-direction: row; align-items: center">
								<view
									style="
										height: 2.5vw;
										width: 2.5vw;
										display: flex;
										align-items: center;
										justify-content: center;
										background-color: #ff0000;
										border-radius: 50%;
										box-shadow: 1px 1px 0.5vw #ff0000;
										margin-right: 1vw;
									"
								>
									<i class="fa-solid fa-trophy" style="color: white"></i>
								</view>
								<text style="font-weight: 700; color: black; font-size: 1.2vw">总督礼物</text>
							</view>
							<view style="font-size: 0.9vw; margin-top: 1vw" v-html="item.gift3.replaceAll('\n', '<br>')"></view>
						</view>
					</view>

					<!-- 冲舰目标礼物（50/100/150/200舰） -->
					<view
						style="display: flex; flex-direction: row; align-items: stretch; width: 100%; font-size: 0.9vw; justify-content: space-around; flex-wrap: wrap"
						v-if="
							(item.gift4 || item.gift5 || item.gift6 || item.gift7) && item.gift4 != 'None' && item.gift5 != 'None' && item.gift6 != 'None' && item.gift7 != 'None'
						"
					>
						<view
							v-if="item.gift4 && item.gift4 != 'None'"
							style="width: 20%; display: flex; flex-direction: column; padding: 1.5%; border-radius: 0.5vw; margin-top: 2vw"
							:style="{
								backgroundColor: item.shipnum >= 50 ? 'rgba(201, 255, 212, 0.1)' : 'rgba(255, 211, 134, 0.1)',
								boxShadow: item.shipnum >= 50 ? '0 0 0.5vw rgba(98, 213, 159, 0.5)' : '0 0 0.5vw rgba(255, 211, 134, 0.5)',
							}"
						>
							<view style="display: flex; flex-direction: row; align-items: center; margin-bottom: 1vw">
								<view style="display: flex; flex-direction: row; align-items: center">
									<view
										style="
											height: 2.5vw;
											width: 2.5vw;
											display: flex;
											align-items: center;
											justify-content: center;
											background-color: #3c9cff;
											border-radius: 50%;
											box-shadow: 1px 1px 0.5vw #3c9cff;
											margin-right: 1vw;
										"
									>
										<i class="fa-solid fa-gift" style="color: white"></i>
									</view>
									<text style="font-size: 1vw; font-weight: 700">50舰礼物</text>
								</view>
								<view
									v-if="item.shipnum >= 50"
									style="margin-left: auto; color: #4ce570; display: flex; flex-direction: row; align-items: center; font-size: 0.9vw"
								>
									已达成
									<i class="fa-solid fa-check-circle" style="margin-top: 0.25vw; margin-left: 0.5vw"></i>
								</view>
								<view v-else style="margin-left: auto; color: #ff9933; display: flex; flex-direction: row; align-items: center; font-size: 0.9vw">
									未达成
									<i class="fa-solid fa-times-circle" style="margin-top: 0.25vw; margin-left: 0.5vw"></i>
								</view>
							</view>
							<view style="color: #2e2f31; margin-top: 0.5vw; font-size: 0.9vw" v-html="item.gift4.replaceAll('\n', '<br>')"></view>
						</view>
						<view
							v-if="item.gift5 && item.gift5 != 'None'"
							style="width: 20%; display: flex; flex-direction: column; padding: 1.5%; border-radius: 0.5vw; margin-top: 2vw"
							:style="{
								backgroundColor: item.shipnum >= 100 ? 'rgba(201, 255, 212, 0.1)' : 'rgba(255, 211, 134, 0.1)',
								boxShadow: item.shipnum >= 100 ? '0 0 0.5vw rgba(98, 213, 159, 0.5)' : '0 0 0.5vw rgba(255, 211, 134, 0.5)',
							}"
						>
							<view style="display: flex; flex-direction: row; align-items: center; margin-bottom: 1vw">
								<view style="display: flex; flex-direction: row; align-items: center">
									<view
										style="
											height: 2.5vw;
											width: 2.5vw;
											display: flex;
											align-items: center;
											justify-content: center;
											background-color: #3c9cff;
											border-radius: 50%;
											box-shadow: 1px 1px 0.5vw #3c9cff;
											margin-right: 1vw;
										"
									>
										<i class="fa-solid fa-gift" style="color: white"></i>
									</view>
									<text style="font-size: 1vw; font-weight: 700">100舰礼物</text>
								</view>
								<view
									v-if="item.shipnum >= 100"
									style="margin-left: auto; color: #4ce570; display: flex; flex-direction: row; align-items: center; font-size: 0.9vw"
								>
									已达成
									<i class="fa-solid fa-check-circle" style="margin-top: 0.25vw; margin-left: 0.5vw"></i>
								</view>
								<view v-else style="margin-left: auto; color: #ff9933; display: flex; flex-direction: row; align-items: center; font-size: 0.9vw">
									未达成
									<i class="fa-solid fa-times-circle" style="margin-top: 0.25vw; margin-left: 0.5vw"></i>
								</view>
							</view>
							<view style="color: #2e2f31; margin-top: 0.5vw; font-size: 0.9vw" v-html="item.gift5.replaceAll('\n', '<br>')"></view>
						</view>
						<view
							v-if="item.gift6 && item.gift6 != 'None'"
							style="width: 20%; display: flex; flex-direction: column; padding: 1.5%; border-radius: 0.5vw; margin-top: 2vw"
							:style="{
								backgroundColor: item.shipnum >= 150 ? 'rgba(201, 255, 212, 0.1)' : 'rgba(255, 211, 134, 0.1)',
								boxShadow: item.shipnum >= 150 ? '0 0 0.5vw rgba(98, 213, 159, 0.5)' : '0 0 0.5vw rgba(255, 211, 134, 0.5)',
							}"
						>
							<view style="display: flex; flex-direction: row; align-items: center; margin-bottom: 1vw">
								<view style="display: flex; flex-direction: row; align-items: center">
									<view
										style="
											height: 2.5vw;
											width: 2.5vw;
											display: flex;
											align-items: center;
											justify-content: center;
											background-color: #3c9cff;
											border-radius: 50%;
											box-shadow: 1px 1px 0.5vw #3c9cff;
											margin-right: 1vw;
										"
									>
										<i class="fa-solid fa-gift" style="color: white"></i>
									</view>
									<text style="font-size: 1vw; font-weight: 700">150舰礼物</text>
								</view>
								<view
									v-if="item.shipnum >= 150"
									style="margin-left: auto; color: #4ce570; display: flex; flex-direction: row; align-items: center; font-size: 0.9vw"
								>
									已达成
									<i class="fa-solid fa-check-circle" style="margin-top: 0.25vw; margin-left: 0.5vw"></i>
								</view>
								<view v-else style="margin-left: auto; color: #ff9933; display: flex; flex-direction: row; align-items: center; font-size: 0.9vw">
									未达成
									<i class="fa-solid fa-times-circle" style="margin-top: 0.25vw; margin-left: 0.5vw"></i>
								</view>
							</view>
							<view style="color: #2e2f31; margin-top: 0.5vw; font-size: 0.9vw" v-html="item.gift6.replaceAll('\n', '<br>')"></view>
						</view>
						<view
							v-if="item.gift7 && item.gift7 != 'None'"
							style="width: 20%; display: flex; flex-direction: column; padding: 1.5%; border-radius: 0.5vw; margin-top: 2vw"
							:style="{
								backgroundColor: item.shipnum >= 200 ? 'rgba(201, 255, 212, 0.1)' : 'rgba(255, 211, 134, 0.1)',
								boxShadow: item.shipnum >= 200 ? '0 0 0.5vw rgba(98, 213, 159, 0.5)' : '0 0 0.5vw rgba(255, 211, 134, 0.5)',
							}"
						>
							<view style="display: flex; flex-direction: row; align-items: center; margin-bottom: 1vw">
								<view style="display: flex; flex-direction: row; align-items: center">
									<view
										style="
											height: 2.5vw;
											width: 2.5vw;
											display: flex;
											align-items: center;
											justify-content: center;
											background-color: #3c9cff;
											border-radius: 50%;
											box-shadow: 1px 1px 0.5vw #3c9cff;
											margin-right: 1vw;
										"
									>
										<i class="fa-solid fa-gift" style="color: white"></i>
									</view>
									<text style="font-size: 1vw; font-weight: 700">200舰礼物</text>
								</view>
								<view
									v-if="item.shipnum >= 200"
									style="margin-left: auto; color: #4ce570; display: flex; flex-direction: row; align-items: center; font-size: 0.9vw"
								>
									已达成
									<i class="fa-solid fa-check-circle" style="margin-top: 0.25vw; margin-left: 0.5vw"></i>
								</view>
								<view v-else style="margin-left: auto; color: #ff9933; display: flex; flex-direction: row; align-items: center; font-size: 0.9vw">
									未达成
									<i class="fa-solid fa-times-circle" style="margin-top: 0.25vw; margin-left: 0.5vw"></i>
								</view>
							</view>
							<view style="color: #2e2f31; margin-top: 0.5vw; font-size: 0.9vw" v-html="item.gift7.replaceAll('\n', '<br>')"></view>
						</view>
						<view
							v-if="item.gift8 && item.gift8 != 'None'"
							style="width: 20%; display: flex; flex-direction: column; padding: 1.5%; border-radius: 0.5vw; margin-top: 2vw"
							:style="{
								backgroundColor: item.shipnum >= 250 ? 'rgba(201, 255, 212, 0.1)' : 'rgba(255, 211, 134, 0.1)',
								boxShadow: item.shipnum >= 250 ? '0 0 0.5vw rgba(98, 213, 159, 0.5)' : '0 0 0.5vw rgba(255, 211, 134, 0.5)',
							}"
						>
							<view style="display: flex; flex-direction: row; align-items: center; margin-bottom: 1vw">
								<view style="display: flex; flex-direction: row; align-items: center">
									<view
										style="
											height: 2.5vw;
											width: 2.5vw;
											display: flex;
											align-items: center;
											justify-content: center;
											background-color: #3c9cff;
											border-radius: 50%;
											box-shadow: 1px 1px 0.5vw #3c9cff;
											margin-right: 1vw;
										"
									>
										<i class="fa-solid fa-gift" style="color: white"></i>
									</view>
									<text style="font-size: 1vw; font-weight: 700">250舰礼物</text>
								</view>
								<view
									v-if="item.shipnum >= 250"
									style="margin-left: auto; color: #4ce570; display: flex; flex-direction: row; align-items: center; font-size: 0.9vw"
								>
									已达成
									<i class="fa-solid fa-check-circle" style="margin-top: 0.25vw; margin-left: 0.5vw"></i>
								</view>
								<view v-else style="margin-left: auto; color: #ff9933; display: flex; flex-direction: row; align-items: center; font-size: 0.9vw">
									未达成
									<i class="fa-solid fa-times-circle" style="margin-top: 0.25vw; margin-left: 0.5vw"></i>
								</view>
							</view>
							<view style="color: #2e2f31; margin-top: 0.5vw; font-size: 0.9vw" v-html="item.gift8.replaceAll('\n', '<br>')"></view>
						</view>
						<view
							v-if="item.gift9 && item.gift9 != 'None'"
							style="width: 20%; display: flex; flex-direction: column; padding: 1.5%; border-radius: 0.5vw; margin-top: 2vw"
							:style="{
								backgroundColor: item.shipnum >= 300 ? 'rgba(201, 255, 212, 0.1)' : 'rgba(255, 211, 134, 0.1)',
								boxShadow: item.shipnum >= 300 ? '0 0 0.5vw rgba(98, 213, 159, 0.5)' : '0 0 0.5vw rgba(255, 211, 134, 0.5)',
							}"
						>
							<view style="display: flex; flex-direction: row; align-items: center; margin-bottom: 1vw">
								<view style="display: flex; flex-direction: row; align-items: center">
									<view
										style="
											height: 2.5vw;
											width: 2.5vw;
											display: flex;
											align-items: center;
											justify-content: center;
											background-color: #3c9cff;
											border-radius: 50%;
											box-shadow: 1px 1px 0.5vw #3c9cff;
											margin-right: 1vw;
										"
									>
										<i class="fa-solid fa-gift" style="color: white"></i>
									</view>
									<text style="font-size: 1vw; font-weight: 700">300舰礼物</text>
								</view>
								<view
									v-if="item.shipnum >= 300"
									style="margin-left: auto; color: #4ce570; display: flex; flex-direction: row; align-items: center; font-size: 0.9vw"
								>
									已达成
									<i class="fa-solid fa-check-circle" style="margin-top: 0.25vw; margin-left: 0.5vw"></i>
								</view>
								<view v-else style="margin-left: auto; color: #ff9933; display: flex; flex-direction: row; align-items: center; font-size: 0.9vw">
									未达成
									<i class="fa-solid fa-times-circle" style="margin-top: 0.25vw; margin-left: 0.5vw"></i>
								</view>
							</view>
							<view style="color: #2e2f31; margin-top: 0.5vw; font-size: 0.9vw" v-html="item.gift9.replaceAll('\n', '<br>')"></view>
						</view>
						<view
							v-if="item.gift8 && item.gift8 != 'None'"
							style="opacity: 0; width: 20%; display: flex; flex-direction: column; padding: 1.5%; border-radius: 0.5vw; margin-top: 2vw"
							:style="{
								backgroundColor: item.shipnum >= 300 ? 'rgba(201, 255, 212, 0.1)' : 'rgba(255, 211, 134, 0.1)',
								boxShadow: item.shipnum >= 300 ? '0 0 0.5vw rgba(98, 213, 159, 0.5)' : '0 0 0.5vw rgba(255, 211, 134, 0.5)',
							}"
						></view>
						<view
							v-if="item.gift8 && item.gift8 != 'None'"
							style="opacity: 0; width: 20%; display: flex; flex-direction: column; padding: 1.5%; border-radius: 0.5vw; margin-top: 2vw"
							:style="{
								backgroundColor: item.shipnum >= 300 ? 'rgba(201, 255, 212, 0.1)' : 'rgba(255, 211, 134, 0.1)',
								boxShadow: item.shipnum >= 300 ? '0 0 0.5vw rgba(98, 213, 159, 0.5)' : '0 0 0.5vw rgba(255, 211, 134, 0.5)',
							}"
						></view>
						<view
							v-if="item.gift8 && item.gift8 != 'None' && (item.gift9 == null || item.gift9 == 'None' || item.gift9 == '')"
							style="opacity: 0; width: 20%; display: flex; flex-direction: column; padding: 1.5%; border-radius: 0.5vw; margin-top: 2vw"
							:style="{
								backgroundColor: item.shipnum >= 300 ? 'rgba(201, 255, 212, 0.1)' : 'rgba(255, 211, 134, 0.1)',
								boxShadow: item.shipnum >= 300 ? '0 0 0.5vw rgba(98, 213, 159, 0.5)' : '0 0 0.5vw rgba(255, 211, 134, 0.5)',
							}"
						></view>
					</view>

					<!-- 备注信息 -->
					<view
						v-if="item.notice && item.notice != 'None'"
						style="
							display: flex;
							flex-direction: column;
							padding: 1.5%;
							background-color: rgba(222, 241, 255, 0.5);
							border-radius: 0.5vw;
							margin-top: 2vw;
							margin-left: 1%;
							width: 95%;
						"
					>
						<text style="font-size: 1vw">备注:{{ item.notice }}</text>
					</view>
				</view>
			</view>

			<!-- 底部空视图（占位） -->
			<view style="opacity: 0; width: 100%; height: 5vw">1</view>
		</u-transition>
	</view>
</template>

<script>
export default {
	data() {
		return {
			list: [],
			show: false,
		}
	},
	methods: {
		pre(e) {
			if (e == null || e.length == 0 || e == 'None') return
			uni.previewImage({
				urls: e.split(';'),
			})
		},
	},
	mounted() {
		uni.request({
			url: '/api/getgift',
			method: 'POST',
			data: {},
			success: (res) => {
				this.list = res.data.data
				this.list.reverse()
				this.show = true
			},
		})
	},
}
</script>

<style>
@import 'https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css';
@font-face {
	font-family: test1;
	src: url('~@/static/test.woff2');
}

.title-container {
	text-align: center;
	margin-bottom: 3vh;
	margin-top: 10vh;
}

.title-container h1 {
	font-family: 'Orbitron', sans-serif;
	font-size: 5vh;
	font-weight: 800;
	margin-bottom: 0.8rem;
	color: #3c9cff;
	text-shadow:
		0 0 10px rgba(60, 156, 255, 0.3),
		0 0 20px rgba(60, 156, 255, 0.1);
}

.title-container p {
	font-size: 1.2rem;
	color: #87cefa;
	letter-spacing: 0.5px;
}
</style>
