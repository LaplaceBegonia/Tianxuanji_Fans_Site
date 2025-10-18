<template>
	<view style="width: 100%; height: 100%; display: flex; flex-direction: row; overflow-y: auto; align-items: flex-start">
		<!--left-->
		<image
			@load="load"
			src="https://image.begonia.cafe/tx/new/image3.webp"
			style="height: 1px; width: 1px; opacity: 0; z-index: -999; position: fixed"
			mode="heightFix"
		></image>
		<u-transition :show="show1" mode="fade-left" style="width: 40%; height: 100%; position: fixed">
			<view style="position: relative; width: 100%">
				<image
					src="https://image.begonia.cafe/tx/new/shadow5.webp"
					style="height: 100vh; position: fixed; top: 0.3vh; left: -6.7vw; width: 100%; position: absolute; z-index: 0; opacity: 0.2"
					mode="heightFix"
				></image>
				<image
					src="https://image.begonia.cafe/tx/new/image7.webp"
					style="height: 100vh; position: fixed; top: 0vh; left: -7vw; width: 100%; position: absolute; z-index: 1"
					mode="heightFix"
				></image>
			</view>
		</u-transition>
		<!--right-->
		<view
			style="
				width: 35vw;
				height: 100%;
				display: flex;
				flex-direction: column;
				align-items: center;
				padding-left: 10%;
				margin-left: 45%;
				padding-top: 5vh;
				padding-bottom: 5vh;
				transition: 1s;
			"
			:style="{ opacity: show1 ? '1' : '0' }"
		>
			<view
				style="
					width: 100%;
					margin-left: 0%;
					margin-top: 10px;
					height: 40px;
					border-radius: 5px;
					font-size: 1.5rem;
					display: flex;
					flex-direction: column;
					height: auto;
					padding: 2%;
					background-color: rgba(255, 255, 255, 0.4);
					border-radius: 20px;
					box-shadow: 0 0 15px rgba(193, 229, 255, 0.8);
				"
				v-if="juge(messagelist)"
			>
				<view
					style="
						border-radius: 20px;
						padding: 2%;
						width: 90%;
						margin-left: 3%;
						height: 100%;
						margin-bottom: 20px;
						margin-top: 20px;
						background-color: rgba(255, 255, 255, 0.9);
						display: flex;
						flex-direction: column;
						box-shadow: 0 0 15px rgba(193, 229, 255, 0.8);
					"
					v-for="(item, index) in messagelist"
					v-if="item.author == '天选姬' || item.author == '天选姬_Official'"
				>
					<view style="display: flex; flex-direction: row; align-items: center">
						<text style="font-size: 1.3rem; color: #446fee; font-weight: 700" v-if="item.title != null && item.title != ''">{{ item.title }}</text>
					</view>
					<text style="font-size: 1rem; color: #5d90c2" :style="{ marginTop: item.title != null && item.title != '' ? '12px' : '0px' }">{{ item.data }}</text>
					<view style="display: flex; flex-direction: row; align-items: center; margin-top: 15px; position: relative; height: 80px">
						<view style="width: 60px; height: 60px; position: relative; margin-right: 10px">
							<img
								referrerpolicy="no-referrer"
								:src="frame"
								style="width: 60px; height: 60px; border-radius: 50%; object-fit: cover; position: absolute; z-index: 2"
							/>
							<img
								referrerpolicy="no-referrer"
								src="https://i1.hdslb.com/bfs/face/97c9320b2eef3e92d25025684301c89493b99a1a.jpg"
								style="
									width: 50px;
									height: 50px;
									border-radius: 50%;
									object-fit: cover;
									position: absolute;
									z-index: 1;
									top: 50%;
									left: 50%;
									transform: translate(-50%, -50%);
								"
							/>
						</view>
						<view style="width: 200px">
							<view style="font-size: 1.4rem; margin-top: 0px; color: black; font-family: sans-serif; color: #4993dd">{{ item.author }}</view>
							<view style="margin-left: auto; font-size: 1.1rem; margin-top: 0px; margin-right: 5%; color: #4993dd">{{ getdate1(item.createtime * 1000) }}</view>
						</view>

						<image style="opacity: 0.4; height: 100px; position: absolute; bottom: -10px; right: 10px" mode="heightFix" src="../../static/2.webp"></image>
					</view>
				</view>
			</view>
			<view
				style="
					width: 100%;
					margin-left: 0%;
					margin-top: 10px;
					height: 40px;
					border-radius: 5px;
					font-size: 1.5rem;
					display: flex;
					flex-direction: column;
					height: auto;
					padding: 2%;
					background-color: rgba(255, 255, 255, 0.4);
					border-radius: 20px;
					box-shadow: 0 0 15px rgba(193, 229, 255, 0.8);
				"
			>
				<view
					style="
						border-radius: 20px;
						padding: 2%;
						width: 90%;
						margin-left: 3%;
						height: 100%;
						margin-bottom: 20px;
						margin-top: 20px;
						background-color: rgba(255, 255, 255, 0.9);
						display: flex;
						flex-direction: column;
						box-shadow: 0 0 15px rgba(193, 229, 255, 0.8);
					"
					v-for="(item, index) in messagelist"
					v-if="item.author != '天选姬' && item.author != '天选姬_Official'"
				>
					<text style="font-size: 1.3rem; color: #446fee; font-weight: 700" v-if="item.title != null && item.title != ''">{{ item.title }}</text>
					<text style="font-size: 1rem; color: #5d90c2" :style="{ marginTop: item.title != null && item.title != '' ? '12px' : '0px' }">{{ item.data }}</text>
					<view style="display: flex; flex-direction: row; align-items: center; margin-top: 15px">
						<view style="font-size: 1.2rem; margin-top: 15px; color: #4993dd">{{ 'by ' + item.author }}</view>
						<view style="margin-left: auto; font-size: 1.2rem; margin-top: 15px; color: #4993dd">{{ getdate(item.createtime * 1000) }}</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			messagelist: {},
			show1: false,
			frame: '',
		}
	},
	methods: {
		close() {
			this.show1 = false
		},
		load() {
			this.show1 = true
		},
		juge(e) {
			for (var x = 0; x < e.length; x++) {
				if (e[x].author == '天选姬' || e[x].author == '天选姬_Official') return true
			}
		},
		getdate1(e) {
			const date = new Date(e)
			const year = date.getFullYear()
			const month = String(date.getMonth() + 1).padStart(2, '0') // 月份从0开始
			const day = String(date.getDate()).padStart(2, '0')
			const hour = String(date.getHours()).padStart(2, '0')
			const min = String(date.getMinutes()).padStart(2, '0')
			const sec = String(date.getSeconds()).padStart(2, '0')
			//return `${year}-${month}-${day} ${hour}:${min}:${sec}`;
			return `${year}-${month}-${day}`
		},
		getdate(timestamp) {
			const date = new Date(timestamp)
			const year = date.getFullYear()
			const month = String(date.getMonth() + 1).padStart(2, '0') // 月份从0开始
			const day = String(date.getDate()).padStart(2, '0')

			return `${year}-${month}-${day}`
		},
	},
	mounted() {
		uni.request({
			url: '/api/getmessage',
			method: 'POST',
			data: {},
			success: (res) => {
				this.messagelist = res.data.data
			},
		})
		uni.request({
			url: '/api/getframe',
			method: 'POST',
			data: {},
			success: (res) => {
				res = res.data
				if (res.new_pendants != null && res.new_pendants.frame != null && res.new_pendants.frame.value != null && res.new_pendants.frame.value != '') {
					this.frame = res.new_pendants.frame.value
				} else {
					this.frame = 'https://i0.hdslb.com/bfs/live/30cc1c9eb6e8b5bd6a8894fd3c2ef019ccce76d1.png'
				}
			},
		})
	},
}
</script>

<style></style>
