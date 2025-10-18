<template>
	<view style="width: 100%; height: 300%; overflow: scroll; height: 100vh; scroll-snap-type: y mandatory; scroll-behavior: smooth" ref="customScrollView" id="wrap">
		<view style="height: 100%; width: 100%; background-color: rgba(206, 238, 255, 0.2); scroll-snap-align: center">
			<u-transition
				duration="750"
				:show="page == 0"
				mode="fade"
				style="width: 100%; height: 100%; display: flex; align-items: center; justify-content: center; flex-direction: column; position: relative"
			>
				<view
					style="width: 60%;margin-top: 10pxheight: 40px;border-radius: 5px;font-size: 3vh;background-color: rgba(255,255,255,0.8);
				display: flex;align-items: center;justify-content: center;padding:1%;padding-top:5px;padding-bottom:5px;
				;box-shadow: 0 0 15px rgba(193, 229, 255, 0.8);"
				>
					<text>{{ '星姬天故事' }}</text>
				</view>
				<view
					style="
						width: 60%;
						margin-top: 10px;
						background-color: rgba(255, 255, 255, 0.8);
						height: auto;
						border-radius: 5px;
						font-size: 1.1rem;
						display: flex;
						flex-direction: column;
						padding: 1%;
						box-shadow: 0 0 15px rgba(193, 229, 255, 0.8);
					"
				>
					<view style="width: 100%; display: flex; flex-direction: column; align-items: center; justify-content: center; margin-top: 10px">
						<image src="/static/星姬天logo.webp" style="height: 13vh; margin-bottom: 20px" mode="heightFix"></image>
						<image src="/static/title.webp" style="width: 40%; margin-bottom: 20px" mode="widthFix"></image>
					</view>
					<view v-html="content" style="font-size: 1.9vh"></view>
				</view>
				<u-icon class="element" name="arrow-down" style="position: absolute; z-index: 1003; left: 49.4vw" size="1.5vw" color="#7cc2ff"></u-icon>
			</u-transition>
		</view>
		<view style="height: 100%; width: 100%; background-color: rgba(125, 255, 227, 0.1); scroll-snap-align: center">
			<u-transition
				duration="750"
				:show="page == 1"
				mode="fade"
				style="width: 100%; height: 100%; display: flex; align-items: center; justify-content: center; flex-direction: column; position: relative"
			>
				<view
					style="width: 60%;margin-top: 10pxheight: 40px;border-radius: 5px;font-size: 3vh;background-color: rgba(255,255,255,0.8);
				display: flex;align-items: center;justify-content: center;padding:1%;padding-top:5px;padding-bottom:5px;
				;box-shadow: 0 0 15px rgba(193, 229, 255, 0.8);"
				>
					<text>{{ '永远陪着璇宝的星姬天们' }}</text>
				</view>
				<view
					style="
						width: 60%;
						margin-top: 10px;
						background-color: rgba(255, 255, 255, 0.8);
						height: auto;
						border-radius: 5px;
						font-size: 1.1rem;
						display: flex;
						flex-direction: row;
						padding: 1%;
						flex-wrap: wrap;
						box-shadow: 0 0 15px rgba(193, 229, 255, 0.8);
					"
				>
					<text style="font-size: 2vh; padding: 1vh" v-for="(item, index) in user" v-if="item.type == 1">{{ item.name }}</text>
					<text style="font-size: 2vh; padding: 1vh" v-for="(item, index) in user" v-if="item.type == 0">{{ item.name }}</text>
					<text style="font-size: 2vh; padding: 1vh">{{ '明前海棠' }}</text>
				</view>
				<view
					style="
						width: 60%;
						margin-top: 10px;
						background-color: rgba(255, 255, 255, 0.8);
						height: auto;
						border-radius: 5px;
						font-size: 1.1rem;
						display: flex;
						flex-direction: row;
						padding: 1%;
						flex-wrap: wrap;
						box-shadow: 0 0 15px rgba(193, 229, 255, 0.8);
					"
				>
					<image src="/static/cat.png" style="width: 3vh; height: 3vh; margin-left: 5px" mode="aspectFill"></image>
					<text style="margin: 5px; margin-left: 5px; width: auto; min-width: 80px; font-size: 2vh">{{ '特别感谢:' }}</text>
					<view style="display: flex; flex-direction: row; align-items: center; flex-wrap: wrap; width: 100%; font-size: 2vh">
						<text style="margin: 5px; margin-left: 5px">{{ '天选姬家的喵' }}</text>
						<text style="margin: 5px; margin-left: 5px">{{ 'RO姬_Official' }}</text>
						<text style="margin: 5px; margin-left: 5px">{{ 'ElevenOfficial_' }}</text>
						<text style="margin: 5px; margin-left: 5px">{{ '槙鸟ZENA' }}</text>
						<text style="margin: 5px; margin-left: 5px">{{ '走路摇ZLY' }}</text>
						<text style="margin: 5px; margin-left: 5px">{{ '小黄鸡吖_' }}</text>
					</view>
				</view>
				<u-icon class="element" name="arrow-down" style="position: absolute; z-index: 1003; left: 49.4vw" size="1.5vw" color="#7cc2ff"></u-icon>
			</u-transition>
		</view>
		<view style="height: 100%; width: 100%; background-color: rgba(206, 238, 255, 0.2); scroll-snap-align: center">
			<u-transition
				duration="750"
				:show="page == 2"
				mode="fade"
				style="width: 100%; height: 100%; display: flex; align-items: center; justify-content: center; flex-direction: column"
			>
				<view
					style="width: 60%;margin-top: 10pxheight: 40px;border-radius: 5px;font-size: 3vh;background-color: rgba(255,255,255,0.8);
				display: flex;align-items: center;justify-content: center;padding:1%;padding-top:5px;padding-bottom:5px;
				;box-shadow: 0 0 15px rgba(193, 229, 255, 0.8);"
				>
					<text>{{ '星姬天签名墙' }}</text>
				</view>
				<view
					style="
						width: 60%;
						margin-top: 10px;
						background-color: rgba(255, 255, 255, 1);
						height: auto;
						border-radius: 5px;
						font-size: 1.1rem;
						display: flex;
						align-items: center;
						justify-content: center;
						padding: 1%;
						box-shadow: 0 0 15px rgba(193, 229, 255, 0.8);
					"
				>
					<view style="width: 95%; height: auto; background-color: rgba(255, 255, 255, 0); border-radius: 5px; overflow: hidden">
						<u-transition duration="1000" :show="page == 2">
							<image src="https://image.begonia.cafe/tx/new/sign.png" style="height: 100%; width: 100%" mode="widthFix"></image>
						</u-transition>
					</view>
				</view>
			</u-transition>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			page: 0,
			height: 0,
			content: '',
			user: [],
			sub: 1,
		}
	},
	methods: {
		close() {
			this.page = -1
		},
		onScroll(e) {
			try {
				let that = this
				let scrollTop = document.querySelector('#wrap').scrollTop
				if (scrollTop == 0) {
					this.page = 0
					this.height = 0
				} else if (this.page == 0 && scrollTop > this.height) {
					this.page = 1
					this.sub = 0
					setTimeout(() => {
						that.sub = 1
					}, 1000)
				} else if (this.page == 1 && scrollTop > this.height && this.sub == 1) {
					this.page = 2
				} else if (this.page == 2 && scrollTop < this.height) {
					this.page = 1
				}
				this.height = scrollTop
			} catch (e) {}
		},
		// 获取滚动高度的核心方法
		getScrollTop() {},
	},
	mounted() {
		addEventListener('scroll', this.onScroll, true)
		this.height = document.querySelector('#wrap').scrollHeight
		uni.request({
			url: '/api/getintroduce',
			method: 'POST',
			data: {},
			success: (res) => {
				this.content = res.data.data[0].content
			},
		})
		uni.request({
			url: '/api/getuserlist',
			method: 'POST',
			data: {},
			success: (res) => {
				this.user = res.data.data
			},
		})
	},
}
</script>

<style>
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
</style>
