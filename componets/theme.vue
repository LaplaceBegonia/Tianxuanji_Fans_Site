<template>
	<view style="width: 100%; height: 100%">
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
				{{ '星姬天文选' }}
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
					border-radius: 10px;
					margin-bottom: 150px;
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
						padding-top: 0px;
						padding-bottom: 20px;
						box-shadow: 0px 0px 5px rgba(60, 156, 255, 0.5);
						background-color: rgba(255, 255, 255, 0.8);
						padding: 10px;
						border-radius: 10px;
					"
					v-for="(item, index) in themelist"
					@click="((info = item), (show = false))"
				>
					<image :src="item.cover" style="height: 120px; min-width: 200px; max-width: 200px; border-radius: 5px; margin-right: 10px" mode="aspectFill"></image>
					<view style="height: 120px; width: 100%; display: flex; flex-direction: column">
						<text style="font-size: 1.8vh">{{ item.title }}</text>
						<u--text size="1.5vh" lines="2" color="rgb(96, 98, 102)" :text="getcontent(item.content)"></u--text>
						<view style="display: flex; flex-direction: row; align-items: center; font-size: 1.5vh; width: 100%">
							<text>{{ '作者:' + item.author }}</text>
						</view>
					</view>
				</view>
				<view
					style="
						padding: 10px;
						width: 30%;
						height: 130px;
						margin-bottom: 10px;
						display: flex;
						flex-direction: row;
						align-items: center;
						padding-top: 0px;
						padding-bottom: 20px;
					"
					v-for="i in 3 - (themelist.length % 3)"
					v-if="3 - (themelist.length % 3) != 3"
				></view>
			</view>
		</u-transition>
		<u-transition
			mode="fade"
			style="width: 100%; height: 100%; overflow-y: auto; padding-top: 0vh; padding-bottom: 0vh; display: flex; flex-direction: column; align-items: center"
			:show="!show"
		>
			<view
				style="
					width: 60vw;
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
					margin-bottom: 2vh;
					padding-bottom: 2vh;
				"
			>
				<view style="display: flex; align-items: center; justify-content: center; width: 100%; font-size: 3vh; margin-bottom: 1vh; position: relative">
					<text>{{ info.title }}</text>
					<view style="width: 100%; height: 100%; display: flex; align-items: center; position: absolute; top: 0; left: 0">
						<view style="width: 2vh; height: 2vh" @click="show = true">
							<u-icon name="arrow-left" size="2vh" style="margin-left: 1%" color="black"></u-icon>
						</view>
					</view>
				</view>
				<view style="display: flex; align-items: center; justify-content: center; width: 100%; font-size: 1.8vh; margin-bottom: 1vh">
					<text>{{ '作者:' + info.author }}</text>
				</view>
				<view v-if="info.content" v-html="info.content.replaceAll('cut-off', '<br>')" style="font-size: 1.8vh"></view>
			</view>
			<view style="height: 5vh; width: 100%"></view>
		</u-transition>
	</view>
</template>

<script>
export default {
	data() {
		return {
			themelist: [],
			show: true,
			info: {},
		}
	},
	methods: {
		getcontent(e) {
			e = e.replaceAll('<br>', ' ')
			e = e.replaceAll('cut-off', ' ')
			return (
				e
					// 移除HTML标签（包括<>内的所有内容）
					.replace(/<[^>]*>?/gm, '')
					// 替换HTML实体（&nbsp;等）为对应字符
					.replace(/&nbsp;/g, ' ')
					.replace(/&amp;/g, '&')
					.replace(/&lt;/g, '<')
					.replace(/&gt;/g, '>')
					.replace(/&quot;/g, '"')
					.replace(/&#39;/g, "'")
					// 合并连续空白字符（空格、换行、制表符等）为单个空格
					.replace(/\s+/g, ' ')
					// 去除首尾空白
					.trim()
			)
		},
	},
	mounted() {
		uni.request({
			url: '/api/getthemelist',
			method: 'POST',
			data: {},
			success: (res) => {
				this.themelist = res.data.data
			},
		})
	},
}
</script>

<style></style>
