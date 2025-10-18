<template>
	<view style="width: 100%; height: 100%; display: flex; flex-direction: row; justify-content: center">
		<!--left-->
		<image
			@load="load"
			src="https://image.begonia.cafe/tx/new/image3.webp"
			style="height: 1px; width: 1px; opacity: 0; z-index: -999; position: fixed"
			mode="heightFix"
		></image>
		<u-transition :show="show1" mode="fade-left" style="width: 40%; height: 100%; position: relative; margin-right: 5%; margin-left: -5%">
			<view style="position: relative; width: 100%">
				<image
					src="https://image.begonia.cafe/tx/new/shadow.webp"
					style="height: 160vh; position: absolute; top: -19.8vh; left: 0.2vw; width: 100%; position: absolute; z-index: 0; opacity: 0.2"
					mode="heightFix"
				></image>
				<image
					src="https://image.begonia.cafe/tx/new/image3.webp"
					style="height: 160vh; position: absolute; top: -20vh; left: 0; width: 100%; position: absolute; z-index: 1"
					mode="heightFix"
				></image>
			</view>
		</u-transition>
		<!--right-->
		<u-transition :show="show1" style="width: 35vw; height: 100vh; overflow-y: auto; margin-left: 5vw">
			<view
				style="
					overflow-y: auto;
					height: auto;
					overflow-x: hidden;
					width: 30vw;
					margin-left: 5%;
					padding: 2.5%;
					padding-top: 1%;
					border-radius: 20px;
					box-shadow: 0 0 15px rgba(193, 229, 255, 0.8);
					margin-top: 5%;
					margin-bottom: 5%;
					display: flex;
					flex-direction: column;
					align-items: center;
					background-color: rgba(255, 255, 255, 0.8);
				"
			>
				<!--title-->
				<view
					:show="show1"
					duration="300"
					style="height: 10%; display: flex; align-items: center; justify-content: center; margin-top: 1vh; position: relative; margin-bottom: 20px"
				>
					<text style="font-size: 4vh; color: #083b7f; font-weight: 700; font-style: italic; opacity: 1">{{ '『 天选姬 』' }}</text>
				</view>
				<!--info-->
				<view
					style="
						display: flex;
						flex-direction: row;
						align-items: center;
						font-size: 2vh;
						color: black;
						width: 30vw;
						margin: 0.5vh;
						font-family: Arial, Helvetica, sans-serif;
						height: auto;
					"
				>
					<view :show="show1" style="display: flex; flex-direction: row; align-items: center; width: 100%">
						<view class="txj-info-grid" style="display: flex; flex-direction: row; flex-wrap: wrap; justify-content: space-around; font-size: 16px">
							<view
								:class="{ 'txj-info-item': item.class != 1, 'txj-info-item1': item.class == 1 }"
								style="width: 40%"
								v-for="(item, index) in info"
								:title="item.label"
								@click="open(item.url)"
							>
								<span class="txj-info-label">{{ item.key }}</span>
								<span class="txj-info-value">{{ item.value }}</span>
							</view>
						</view>
					</view>
				</view>
				<view style="display: flex; flex-direction: row; align-items: center; width: 30vw; margin-top: 0px; height: auto">
					<view style="width: 100%; display: flex; flex-direction: column; font-size: 1.8vh; margin-top: 0vh; font-style: italic; color: #414141">
						<text>
							{{
								'『 天选姬原名“小璇”，原本是某科技公司的实习生，在一次数码产品评测中意外解锁了天选游戏本的神秘力量，被来自未来世界的可能是来自美丽富饶的阿苏斯星的猫咪老师选定，签订“天选契约”，获得了具备神秘力量的天选铠甲变身为天选姬，开始对抗黑暗势力的漫长旅程。'
							}}
						</text>
						<text>
							{{
								'天选姬不仅战斗能力高强、意识强大，同时也是一枚科技区学霸，博闻强识，不论是软件的各种隐藏操作，还是硬件养护的神仙小技巧，对她来说都不在话下。闲暇之余，她更是一位号称拥有百万衣橱的穿搭达人，也是精通各种游戏的硬核玩家。'
							}}
						</text>
						<text>{{ '百变天选姬，你喜欢的样子她都有！』' }}</text>
					</view>
				</view>
			</view>
		</u-transition>
	</view>
</template>

<script>
export default {
	data() {
		return {
			show: false,
			show1: false,
			info: [
				{
					key: '本名',
					value: '天选姬',
					label: '星姬天们的老婆',
					class: 1,
				},
				{
					key: '别名',
					value: '璇宝、小璇、阿姬、电竞美杜莎、磕学家、"穹顶之御"',
					label: '穹顶之御是谁家小孩?',
					class: 1,
				},
				{
					key: '瞳色',
					value: '湛青绿瞳',
				},
				{
					key: '发色',
					value: '月白灰发',
				},
				{
					key: '身高',
					value: '165cm',
				},
				{
					key: '年龄',
					value: '别问，问就18岁',
					label: '88岁老太',
					class: 1,
				},
				{
					key: '生日',
					value: '3月16日',
				},
				{
					key: '星座',
					value: '双鱼座',
				},
				{
					key: '出道日',
					value: '3月17日',
				},
				{
					key: '粉丝数',
					value: '待统计',
				},
				{
					key: '粉丝勋章',
					value: '星姬天',
				},
				{
					key: 'Tag',
					value: '天选一家亲',
					url: 'https://www.bilibili.com/v/topic/detail/?topic_id=1276331',
					class: 1,
				},
			],
		}
	},
	methods: {
		load(e) {
			this.show1 = true
		},
		close() {
			this.show1 = false
		},
		open(e) {
			if (e != null) window.open(e)
		},
	},
	mounted() {
		uni.request({
			url: '/api/getfans',
			method: 'POST',
			data: {},
			success: (res) => {
				this.info[9].value = res.data.data
			},
		})
		let that = this
		setTimeout(() => {
			that.show = true
		}, 500)
	},
}
</script>

<style>
/* 鼠标悬停时显示提示框 */
.txj-info-grid:hover::after {
	opacity: 0;
}
.txj-info-grid {
	display: grid;
	grid-template-columns: repeat(2, 1fr);
	gap: 15px;
	margin-bottom: 25px;
}

.txj-info-item {
	padding: 10px 15px;
	background-color: rgba(255, 255, 255, 0.8);
	border-radius: 8px;
	box-shadow: 0 2px 6px rgba(0, 0, 0, 0.05);
	transition: background-color 0.3s ease;
}
.txj-info-item1 {
	padding: 10px 15px;
	background-color: rgba(255, 255, 255, 0.8);
	border-radius: 8px;
	box-shadow: 0 2px 6px rgba(0, 0, 0, 0.05);
	transition: background-color 0.3s ease;
}
.txj-info-item:hover {
	background-color: rgba(230, 247, 255, 0.8);
}
.txj-info-item1:hover {
	background-color: rgba(250, 240, 255, 0.8);
}
.txj-info-label {
	display: block;
	font-weight: 600;
	color: #2563eb;
	margin-bottom: 5px;
}

.txj-info-value {
	color: #334155;
}
text {
	user-select: text;
}
</style>
