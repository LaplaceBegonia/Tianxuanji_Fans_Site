<template>
	<view
		@mousewheel="scroll"
		style="width: 100vw; height: 100vh; background: linear-gradient(to bottom, #eff9ff, rgba(155, 255, 244, 0.3)); overflow: hidden; position: relative; font-family: test"
	>
		<view class="magic-bg" style="z-index: 0; position: fixed; top: 0; left: 0; width: 100%; height: 100%"></view>
		<!--bg-->
		<image
			src="https://image.begonia.cafe/tx/new/bg/bg1.webp"
			style="width: 20vw; position: fixed; left: 0; top: 0; transform: rotate(180deg); z-index: 0; opacity: 0.2"
			mode="widthFix"
		></image>
		<image src="https://image.begonia.cafe/tx/new/bg/bg2.webp" style="width: 30vw; position: fixed; right: 0; bottom: 0; z-index: 0" mode="widthFix"></image>
		<image src="https://image.begonia.cafe/tx/new/bg/bg3.png" style="width: 10vw; position: fixed; left: 30vw; top: 5vh; z-index: 0; opacity: 0.8" mode="widthFix"></image>
		<image src="https://image.begonia.cafe/tx/new/bg/bg3.png" style="width: 10vw; position: fixed; left: 5vw; bottom: 5vh; z-index: 0; opacity: 0.8" mode="widthFix"></image>
		<image src="https://image.begonia.cafe/tx/new/bg/bg4.png" style="width: 10vw; position: fixed; right: 0vw; top: 5vh; z-index: 0" mode="widthFix"></image>
		<image src="https://image.begonia.cafe/tx/new/bg/bg5.png" style="width: 7vw; position: fixed; right: 20vw; top: 5vh; z-index: 0" mode="widthFix"></image>
		<image src="https://image.begonia.cafe/tx/new/cat.png" style="width: 12vw; position: fixed; right: 52vw; bottom: 0vh; z-index: 0; opacity: 0.6" mode="widthFix"></image>
		<image
			src="https://image.begonia.cafe/tx/new/bg/bg.webp"
			style="width: 100vw; height: 100vh; position: fixed; left: 0; top: 0; z-index: 0; opacity: 0.6"
			mode="aspectFill"
		></image>
		<!--page-->
		<!--天选姬-->
		<index ref="index" v-if="page == 0" style="width: 100%; height: 100%; z-index: 1; position: relative"></index>
		<!--日程表-->
		<date ref="date" v-if="page == 1" style="width: 100%; height: 100%; z-index: 1; position: relative"></date>
		<!--数据分析-->
		<data1 v-if="page == 2" style="width: 100%; height: 100%; z-index: 1; position: relative"></data1>
		<!--切片-->
		<video1 v-if="page == 3" style="width: 100%; height: 100%; z-index: 1; position: relative"></video1>
		<!--文选-->
		<theme v-if="page == 4" style="width: 100%; height: 100%; z-index: 1; position: relative"></theme>
		<!--素材-->
		<emoji v-if="page == 5" style="width: 100%; height: 100%; z-index: 1; position: relative"></emoji>
		<!--留言-->
		<message ref="message" v-if="page == 6" style="width: 100%; height: 100%; z-index: 1; position: relative"></message>
		<!--星姬天-->
		<fans ref="fans" v-if="page == 7" style="width: 100%; height: 100%; z-index: 1; position: relative"></fans>
		<!--天选百科-->
		<info ref="info" v-if="page == 8" style="width: 100%; height: 100%; z-index: 1; position: relative"></info>
		<!--大航海-->
		<gift v-if="page == 9" style="width: 100%; height: 100%; z-index: 1; position: relative"></gift>
		<!--相关链接-->
		<url v-if="page == 10" style="width: 100%; height: 100%; z-index: 1; position: relative"></url>
		<!--right-->
		<view style="height: 50vh; width: 5vw; right: 0; top: 25vh; position: fixed; z-index: 99; border-radius: 0px">
			<div class="nav-right">
				<div class="nav-item" :class="{ active: page == 0 }" @click="close(0, 'info')">
					<i class="fa-solid fa-heart"></i>
					<span>天选姬</span>
				</div>
				<div class="nav-item" :class="{ active: page == 8 }" @click="close(8, 'info')">
					<i class="fa-solid fa-book"></i>
					<span>天选百科</span>
				</div>
				<div class="nav-item" :class="{ active: page == 1 }" @click="close(1, 'info')">
					<i class="fa-solid fa-calendar"></i>
					<span>日程表</span>
				</div>
				<div class="nav-item" :class="{ active: page == 2 }" @click="close(2, 'info')">
					<i class="fa-solid fa-chart-line"></i>
					<span>数据</span>
				</div>
				<div class="nav-item" :class="{ active: page == 3 }" @click="close(3, 'info')">
					<i class="fa-solid fa-film"></i>
					<span>切片</span>
				</div>
				<div class="nav-item" :class="{ active: page == 4 }" @click="close(4, 'info')">
					<i class="fa-solid fa-pencil"></i>
					<span>文选</span>
				</div>
				<div class="nav-item" :class="{ active: page == 5 }" @click="close(5, 'info')">
					<i class="fa-solid fa-image"></i>
					<span>素材</span>
				</div>
				<div class="nav-item" :class="{ active: page == 6 }" @click="close(6, 'info')">
					<i class="fa-solid fa-comment-dots"></i>
					<span>留言</span>
				</div>
				<div class="nav-item" :class="{ active: page == 7 }" @click="close(7, 'info')">
					<i class="fa-solid fa-star"></i>
					<span>星姬天</span>
				</div>
				<div class="nav-item" :class="{ active: page == 9 }" @click="close(9, 'info')">
					<i class="fa-solid fa-rocket"></i>
					<span>大航海</span>
				</div>
				<div class="nav-item" :class="{ active: page == 10 }" @click="close(10, 'info')">
					<i class="fa-solid fa-code" />
					<span>相关链接</span>
				</div>
				<div class="nav-item" :class="{ active: current === '华硕天选' }" @click="show = true">
					<i class="fa-solid fa-calendar-week"></i>
					<span>本周周表</span>
				</div>
				<div class="nav-item" :class="{ active: current === '华硕天选' }" @click="shownotice = true">
					<i class="fa-solid fa-bullhorn"></i>
					<span>公告信息</span>
				</div>
				<div class="nav-item" :class="{ active: current === '华硕天选' }" @click="relaunch('/pages/index/index')">
					<i class="fa-solid fa-history"></i>
					<span>返回旧版</span>
				</div>
				<div class="nav-item" :class="{ active: current === '华硕天选' }" @click="openpage('https://www.asus.com.cn/laptops/for-gaming/tuf-gaming/')">
					<i class="fa-solid fa-laptop"></i>
					<span>华硕天选</span>
				</div>
			</div>
		</view>
		<!--date-->
		<u-popup :show="show && showinfo" @close="show = false" mode="center" round="10" bgColor="transparent" zIndex="999">
			<view
				style="
					height: 80vh;
					width: auto;
					background-color: rgba(255, 255, 255, 0.95);
					display: flex;
					align-items: center;
					flex-direction: column;
					border-radius: 10px;
					padding: 10px;
				"
			>
				<text style="font-size: 4vh; font-weight: 700; color: #3c9cff; text-shadow: #86d1ff 2px 1.5px 3px; margin-top: 3vh; margin-bottom: 3vh">{{ '本周日程表' }}</text>
				<view style="display: flex; position: relative; width: auto; height: auto">
					<image
						src="https://image.begonia.cafe/tx/date.webp"
						style="width: 100%; height: 60vh"
						mode="heightFix"
						@click="openpage('https://live.bilibili.com/2058234')"
					></image>
				</view>
			</view>
		</u-popup>
		<!---->
		<u-popup :show="shownotice" @close="shownotice = false" mode="center" round="5" bgColor="transparent" zIndex="999">
			<view
				style="
					height: 70vh;
					overflow-y: auto;
					padding: 20px;
					width: 30vw;
					background-color: rgba(255, 255, 255, 0.95);
					display: flex;
					align-items: center;
					flex-direction: column;
					border-radius: 10px;
				"
			>
				<view
					style="width: 100%; display: flex; flex-direction: column; padding-bottom: 10px; border-bottom: 0.5px solid #efefef; margin-bottom: 10px"
					v-for="(item, index) in list"
					v-if="item.top"
				>
					<view style="display: flex; flex-direction: row; align-items: center; justify-content: space-between">
						<view style="font-size: 2.1vh; font-weight: 700; margin-bottom: 10px">{{ item.title }}</view>
						<view style="padding: 5px 10px 5px 10px; font-size: 1.3vh; color: white; background-color: #27cead; border-radius: 30px">{{ '置顶' }}</view>
					</view>

					<view style="font-size: 1.6vh; color: #404144; margin-bottom: 10px">{{ item.data }}</view>
					<view style="font-size: 1.6vh; color: #888a90; display: flex; flex-direction: row; align-items: center; justify-content: space-between; margin-bottom: 10px">
						<text style="font-size: 1.6vh">{{ item.author }}</text>
						<text style="font-size: 1.7vh">{{ item.time }}</text>
					</view>
				</view>
				<view
					style="width: 100%; display: flex; flex-direction: column; padding-bottom: 10px; border-bottom: 0.5px solid #efefef"
					v-for="(item, index) in list"
					v-if="!item.top"
				>
					<view style="font-size: 2.1vh; font-weight: 700; margin-bottom: 10px">{{ item.title }}</view>
					<view style="font-size: 1.6vh; color: #404144; margin-bottom: 10px">{{ item.data }}</view>
					<view style="font-size: 1.6vh; color: #888a90; display: flex; flex-direction: row; align-items: center; justify-content: space-between">
						<text style="font-size: 1.6vh">{{ item.author }}</text>
						<text style="font-size: 1.7vh">{{ item.time }}</text>
					</view>
				</view>
			</view>
		</u-popup>
		<!---->
		<view
			v-if="showvideo"
			@click="closevideo1()"
			style="width: 100vw; height: 100vh; background-color: #27cead; position: fixed; top: 0; left: 0; object-fit: cover; transition: 1s"
			:style="{ opacity: op, zIndex: zindex }"
		>
			<view
				style="
					height: 100vh;
					width: 100vw;
					position: fixed;
					z-index: 1001;
					background-color: rgba(0, 0, 0, 0.5);
					display: flex;
					align-items: center;
					justify-content: center;
				"
			>
				<view
					:style="{ opacity: op1 }"
					style="width: 100vw; display: flex; flex-direction: row; align-items: center; justify-content: center; margin-top: -15vh; transition: 1s"
				>
					<image src="/static/doro2.webp" style="opacity: 0.85; width: 30vh; height: 30vh; transition: 0.5s; margin-top: 10vh" mode="aspectFit"></image>
					<image
						src="/static/title.webp"
						style="width: 30vw; margin-bottom: 20px; margin-top: 15vh; margin-left: 2vw; margin-right: 2vw; opacity: 0.85"
						mode="widthFix"
					></image>
					<image src="/static/doro1.webp" style="opacity: 0.85; width: 30vh; height: 30vh; transition: 0.5s; margin-top: 10vh" mode="aspectFit"></image>
				</view>
			</view>
			<view style="width: 100vw; height: 70px; position: fixed; z-index: 1002; backdrop-filter: blur(10px); transition: 1s" :style="{ opacity: op1 == 0.8 ? '1' : '0' }">
				<view
					style="
						width: 50%;
						margin-left: 25%;
						height: 100%;
						display: flex;
						align-items: center;
						opacity: 0.7;
						justify-content: space-around;
						flex-direction: row;
						color: white;
						font-size: 16px;
					"
				>
					<text>天选姬非官方粉丝站</text>
					<text @click="close(0, 'info')" class="t1">天选姬</text>
					<text @click="close(8, 'info')" class="t1">天选百科</text>
					<text @click="close(1, 'info')" class="t1">日程表</text>
					<text @click="close(2, 'info')" class="t1">数据</text>
					<text @click="close(3, 'info')" class="t1">切片</text>
					<text @click="close(4, 'info')" class="t1">文选</text>
					<text @click="close(5, 'info')" class="t1">素材</text>
					<text @click="close(6, 'info')" class="t1">留言</text>
					<text @click="close(7, 'info')" class="t1">星姬天</text>
					<text @click="close(9, 'info')" class="t1">大航海</text>
					<text @click="close(10, 'info')" class="t1">相关链接</text>
				</view>
				<image src="/static/星姬天logo.webp" style="height: 50px; position: absolute; top: 10px; left: 5vw; opacity: 0.8" mode="heightFix"></image>
				<image src="/static/title.webp" style="height: 50px; position: absolute; top: 10px; left: 8.5vw; opacity: 0.8" mode="heightFix"></image>
			</view>
			<view style="position: fixed; z-index: 1000" v-html="temp"></view>
			<u-icon class="element" name="arrow-down" style="position: fixed; z-index: 1003; left: 49.4vw" size="1.2vw" color="white"></u-icon>
			<image
				src="/static/doro.gif"
				style="height: 120px; width: 100px; position: absolute; z-index: 1003; bottom: 10px"
				mode="heightFix"
				:class="{ right: !showdoro1, left: showdoro1 }"
			></image>
			<image
				src="/static/doro1.gif"
				style="height: 120px; width: 100px; position: absolute; z-index: 1003; bottom: 10px"
				mode="heightFix"
				:class="{ right: !showdoro2, left1: showdoro2 }"
			></image>
			<image
				src="/static/doro2.gif"
				style="height: 120px; width: 100px; position: absolute; z-index: 1003; bottom: 10px"
				mode="heightFix"
				:class="{ right: !showdoro3, left2: showdoro3 }"
			></image>
		</view>
	</view>
</template>
<script>
import index from '../componets/index.vue'
import date from '../componets/date.vue'
import info from '../componets/info.vue'
import data1 from '../componets/data.vue'
import video1 from '../componets/video.vue'
import message from '../componets/message.vue'
import theme from '../componets/theme.vue'
import emoji from '../componets/emoji.vue'
import fans from '../componets/fans.vue'
import gift from '../componets/gift.vue'
import url from '../componets/url.vue'
export default {
	components: {
		index,
		date,
		info,
		data1,
		video1,
		message,
		theme,
		emoji,
		fans,
		gift,
		url,
	},
	data() {
		return {
			BASE_CONFIG: {
				lerps: {
					dot: 1,
					circle: 0.18,
					custom: 0.23,
				},
				scale: {
					ratio: 0.18,
					min: 0.5,
					max: 1,
				},
				opacity: 0.1,
			},
			temp: "<video muted  preload autoplay loop style='width: 100vw;height:100vh;object-fit: cover' ><source src='https://image.begonia.cafe/tx/bg/bg.mp4' type='video/mp4'><source src='https://image.begonia.cafe/tx/bg/bg.mp4' type='video/ogg'></video>",
			list: [],
			showvideo: true,
			zindex: 999,
			op: 1,
			op1: 0,
			current: '',
			page: 0,
			showinfo: true,
			show: false,
			shownotice: false,
			show1: false,
			show2: false,
			show3: false,
			show4: false,
			show5: false,
			show6: false,
			show7: false,
			show8: false,
			show9: false,
			show10: false,
			show11: false,
			showdoro1: false,
			showdoro2: false,
			showdoro3: false,
			showdorosub: false,
			showdorosub1: true,
			timer2: null,
		}
	},
	methods: {
		showdoro() {
			let that = this
			that.showdorosub = true
			var sub = Math.floor(Math.random() * 100)
			if (sub <= 33 && sub > 0) {
				that.showdoro1 = true
				setTimeout(() => {
					that.showdorosub = false
					setTimeout(() => {
						that.showdoro1 = false
						that.showdorosub1 = true
					}, 10)
				}, 6000)
			} else if (sub <= 66 && sub > 33) {
				that.showdoro2 = true
				setTimeout(() => {
					that.showdorosub = false
					setTimeout(() => {
						that.showdoro2 = false
						that.showdorosub1 = true
					}, 10)
				}, 3000)
			} else {
				that.showdoro3 = true
				setTimeout(() => {
					that.showdorosub = false
					setTimeout(() => {
						that.showdoro3 = false
						that.showdorosub1 = true
					}, 10)
				}, 4500)
			}
		},
		scroll(e) {
			this.closevideo1()
		},
		closevideo1() {
			this.op = 0
			this.zindex = -1
			let that = this
			setTimeout(() => {
				that.showvideo = false
			}, 1000)
		},
		close(e, i) {
			if (this.page == 0 && e != 0) {
				this.$refs.index.close()
			}
			if (this.page == 1 && e != 1) {
				this.$refs.date.close()
			}
			if (this.page == 8 && e != 8) {
				this.$refs.info.close()
			}
			if (this.page == 6 && e != 6) {
				this.$refs.message.close()
			}
			if (this.page == 7 && e != 7) {
				this.$refs.fans.close()
			}
			let that = this
			setTimeout(() => {
				that.page = e
			}, 300)
		},
		back() {
			uni.navigateBack()
		},
		openpage(e) {
			window.open(e)
		},
		relaunch(e) {
			uni.setStorageSync('index', 'old')
			uni.reLaunch({
				url: e,
			})
		},
		pre(e) {
			uni.previewImage({
				urls: [e],
			})
		},
		load() {
			let that = this
			setTimeout(() => {
				that.show1 = true
			}, 50)
			setTimeout(() => {
				that.show2 = true
			}, 100)
			setTimeout(() => {
				that.show3 = true
			}, 150)
			setTimeout(() => {
				that.show4 = true
			}, 200)
			setTimeout(() => {
				that.show5 = true
			}, 250)
			setTimeout(() => {
				that.show6 = true
			}, 300)
			setTimeout(() => {
				that.show7 = true
			}, 350)
			setTimeout(() => {
				that.show8 = true
			}, 400)
			setTimeout(() => {
				that.show9 = true
			}, 450)
			setTimeout(() => {
				that.show10 = true
			}, 500)
			setTimeout(() => {
				that.show11 = true
			}, 500)
		},
		closevideo() {
			uni.setStorageSync('showvideo', 1)
			this.closevideo1()
		},
	},
	onLoad() {
		let that = this
		this.timer2 = setInterval(() => {
			if (that.showdorosub1 == true) {
				that.showdorosub = 10000
				var sub = Math.floor(Math.random() * 2000)
				if (sub <= 100 && that.showdorosub1) {
					that.showdorosub1 = false
					that.showdoro()
				}
			}
		}, 3000)
		const systemInfo = uni.getSystemInfoSync()
		const isPortrait = systemInfo.screenHeight > systemInfo.screenWidth
		this.load()
		if (isPortrait) {
			uni.reLaunch({
				url: '/pages/index/index',
			})

			return
		}
		if (uni.getStorageSync('index') == null) {
			uni.setStorageSync('index', 'new')
		}
		if (uni.getStorageSync('index') == 'old') {
			uni.reLaunch({
				url: '/pages/index/index',
			})
		}
		setTimeout(() => {
			that.op1 = 0.8
		}, 100)
		uni.request({
			url: '/api/getnotice',
			method: 'POST',
			data: {},
			success: (res) => {
				this.list = res.data.data
				this.list.reverse()
				if (
					uni.getStorageSync('shownotice') != true ||
					uni.getStorageSync('noticelength') == null ||
					(uni.getStorageSync('noticelength') != null && this.list.length != uni.getStorageSync('noticelength'))
				) {
					uni.setStorageSync('shownotice', true)
					uni.setStorageSync('noticelength', this.list.length)
					this.shownotice = true
				}
			},
		})
	},
	onShow() {},
}
</script>

<style>
.t1:hover {
	color: #3c9cff;
}
.t1 {
	transition: 0.5s;
}
.magic-bg {
	background-image: linear-gradient(rgba(93, 230, 220, 0.1) 1px, transparent 1px), linear-gradient(90deg, rgba(93, 230, 220, 0.1) 1px, transparent 1px);
	background-size: 40px 40px;
	background-position: center center;
	min-height: 100vh;
}
.nav-right {
	position: fixed;
	right: 20px;
	top: 50%;
	transform: translateY(-50%);
	display: flex;
	flex-direction: column;
	gap: 10px;
	background-color: rgba(255, 255, 255, 0.8);
	padding: 15px;
	border-radius: 20px;
	box-shadow: 0 5px 15px rgba(108, 156, 255, 0.2);
	backdrop-filter: blur(5px);
}

.nav-item {
	display: flex;
	align-items: center;
	gap: 8px;
	padding: 8px 12px;
	border-radius: 12px;
	cursor: pointer;
	transition: all 0.3s ease;
	color: #666;
}
@keyframes changeColor {
	0% {
		bottom: 2vh;
	}
	25% {
		bottom: 3vh;
	}
	50% {
		bottom: 2vh;
	}
	75% {
		bottom: 3vh;
	}
	100% {
		bottom: 2vh;
	}
}
.element {
	animation: changeColor 2s ease-in-out infinite;
}
.nav-item:hover {
	background-color: rgba(108, 156, 255, 0.1);
	transform: translateX(-5px);
}

.nav-item.active {
	background: linear-gradient(135deg, #6c9cff, #b6d0ff);
	color: white;
	font-weight: bold;
	box-shadow: 0 3px 8px rgba(108, 156, 255, 0.3);
}

.nav-item i {
	width: 20px;
	text-align: center;
}
@font-face {
	font-family: test;
	src: url('~@/static/font.woff2');
}
.right {
	right: -120px;
}
.left {
	right: 100vw;
	transition: 5s linear;
}
.left1 {
	right: 100vw;
	transition: 2s linear;
}
.left2 {
	right: 100vw;
	transition: 3.5s linear;
}
</style>
