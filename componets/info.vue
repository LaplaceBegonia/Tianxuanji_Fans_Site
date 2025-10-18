<template>
	<view style="width: 100%; height: 100%; overflow-y: auto; display: flex; flex-direction: row; align-items: flex-start" class="class-name">
		<image src="https://image.begonia.cafe/tx/全身图.webp" style="height: 1px; width: 1px; opacity: 0; position: fixed; top: 0; left: 0" mode="aspectFill" @load="load"></image>
		<image
			src="https://image.begonia.cafe/tx/2024新春装扮.webp"
			style="height: 1px; width: 1px; opacity: 0; position: fixed; top: 0; left: 0"
			mode="aspectFill"
			@load="load"
		></image>
		<image
			src="https://image.begonia.cafe/tx/2025年机甲装扮.webp"
			style="height: 1px; width: 1px; opacity: 0; position: fixed; top: 0; left: 0"
			mode="aspectFill"
			@load="load"
		></image>
		<image
			src="https://image.begonia.cafe/tx/new/shadow1.webp"
			style="height: 1px; width: 1px; opacity: 0; position: fixed; top: 0; left: 0"
			mode="aspectFill"
			@load="load"
		></image>
		<image
			src="https://image.begonia.cafe/tx/new/shadow2.webp"
			style="height: 1px; width: 1px; opacity: 0; position: fixed; top: 0; left: 0"
			mode="aspectFill"
			@load="load"
		></image>
		<image
			src="https://image.begonia.cafe/tx/new/shadow4.webp"
			style="height: 1px; width: 1px; opacity: 0; position: fixed; top: 0; left: 0"
			mode="aspectFill"
			@load="load"
		></image>

		<u-transition :show="show >= 6 && show1 == 0" mode="fade-left" style="width: 40%; height: 100vh; position: fixed; top: 0; left: -2.5%; padding-top: 0vh">
			<view style="height: 20vh; width: 100%"></view>
			<image
				@click="addshow"
				src="https://image.begonia.cafe/tx/全身图.webp"
				style="height: 150vh; width: 45vw; position: absolute; top: 0; left: 0"
				mode="heightFix"
			></image>
			<image
				src="https://image.begonia.cafe/tx/new/shadow2.webp"
				style="height: 150vh; width: 45vw; position: absolute; top: 0.5vh; left: 0.5vw; z-index: -1; opacity: 0.1"
				mode="heightFix"
			></image>
		</u-transition>
		<u-transition :show="show >= 6 && show1 == 1" mode="fade-left" style="width: 40%; height: 100vh; position: fixed; top: 0; left: -2.5%; padding-top: 0vh">
			<view style="height: 20vh; width: 100%"></view>
			<image
				@click="addshow"
				src="https://image.begonia.cafe/tx/2024新春装扮.webp"
				style="height: 150vh; width: 45vw; position: absolute; top: 1vh; left: 5vw"
				mode="heightFix"
			></image>
			<image
				src="https://image.begonia.cafe/tx/new/shadow1.webp"
				style="height: 150vh; width: 45vw; position: absolute; top: 1.5vh; left: 5.5vw; z-index: -1; opacity: 0.1"
				mode="heightFix"
			></image>
		</u-transition>
		<u-transition :show="show >= 6 && show1 == 2" mode="fade-left" style="width: 40%; height: 100vh; position: fixed; top: 0; left: -2.5%; padding-top: 0vh">
			<view style="height: 20vh; width: 100%"></view>
			<image
				@click="addshow"
				src="https://image.begonia.cafe/tx/2025年机甲装扮.webp"
				style="height: 150vh; width: 45vw; position: absolute; top: 1vh; left: 5vw"
				mode="heightFix"
			></image>
			<image
				src="https://image.begonia.cafe/tx/new/shadow4.webp"
				style="height: 150vh; width: 45vw; position: absolute; top: 1.5vh; left: 5.5vw; z-index: -1; opacity: 0.1"
				mode="heightFix"
			></image>
		</u-transition>
		<u-transition
			:show="show >= 6"
			mode="fade-right"
			style="
				margin-right: 12%;
				width: 30vw;
				min-width: 30vw;
				height: auto;
				display: flex;
				align-items: center;
				justify-content: center;
				flex-direction: column;
				margin-left: auto;
			"
		>
			<view
				v-html="info"
				style="
					width: 30vw;
					height: auto;
					margin-top: 3vh;
					border-radius: 20px;
					box-shadow: 0 0 15px rgba(193, 229, 255, 0.8);
					padding-bottom: 5vh;
					background-color: rgba(255, 255, 255, 0.8);
					padding: 5%;
				"
			></view>
		</u-transition>
	</view>
</template>

<script>
export default {
	data() {
		return {
			info: '',
			baseurl: '/api/',
			show: 0,
			show1: 0,
		}
	},
	mounted() {
		var randomNumber = Math.floor(Math.random() * 1000) + 1
		if (randomNumber >= 0 && randomNumber < 333) this.show1 = 0
		if (randomNumber >= 333 && randomNumber < 666) this.show1 = 1
		if (randomNumber >= 666 && randomNumber <= 1000) this.show1 = 2
		this.getmore()
	},
	methods: {
		close() {
			this.show = 0
		},
		getmore() {
			uni.request({
				url: this.baseurl + 'getinfo',
				method: 'POST',
				data: {},
				success: (res) => {
					this.info = res.data.data[0].info
					this.show++
				},
			})
		},
		load() {
			this.show++
		},
		addshow() {
			if (this.show1 == 2) this.show1 = 0
			else this.show1++
		},
	},
}
</script>

<style>
.class-name {
	overflow: scroll;
	box-sizing: border-box;
}
/*定义整体的宽度*/
.class-name::-webkit-scrollbar {
	width: 30px;
}
/*定义滚动条轨道*/
.class-name::-webkit-scrollbar-track {
	border-radius: 5px;
}
/*定义滑块*/
.class-name::-webkit-scrollbar-thumb {
	border-radius: 5px;
	background: rgba(27, 140, 236, 0.5);
}
view {
	user-select: text;
}
</style>
