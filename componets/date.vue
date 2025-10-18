<template>
	<view style="width: 100%; height: 100%; display: flex; align-items: center; justify-content: center; flex-direction: column; overflow-y: auto">
		<u-transition :show="show1" mode="fade" style="width: 100%; height: 100%; display: flex; align-items: center; flex-direction: column">
			<view
				style="
					font-family: 'Orbitron', sans-serif;
					font-size: 4vh;
					font-weight: 800;
					margin-bottom: 2vh;
					margin-top: 10vh;
					color: #3c9cff;
					text-shadow: 0 0 10px rgba(60, 156, 255, 0.3);
				"
			>
				{{ '日程表' }}
			</view>
			<view
				style="
					height: auto;
					width: 80vw;
					border-radius: 0px;
					background-color: rgba(255, 255, 255, 0.35);
					margin-top: 2vh;
					display: flex;
					flex-wrap: wrap;
					padding: 10px;
					justify-content: space-between;
					box-shadow: 0 0 15px rgba(193, 229, 255, 0.8);
					border-radius: 20px;
				"
			>
				<view style="display: flex; flex-direction: row; align-items: center; width: 100%; font-size: 1.8vh; margin-top: 0.5vh; margin-bottom: 0.5vh">
					<view style="color: #6e5bd8; margin-right: 1.5vh" @click="type = -1">{{ '全部:' + num }}</view>
					<view style="color: #9e2d73; margin-right: 1.5vh" @click="type = 0">{{ '杂谈:' + typelist[0] }}</view>
					<view style="color: #7400da; margin-right: 1.5vh" @click="type = 1">{{ '歌回:' + typelist[1] }}</view>
					<view style="color: #326699; margin-right: 1.5vh" @click="type = 2">{{ '游戏回:' + typelist[2] }}</view>
					<view style="color: #287a7a; margin-right: 1.5vh" @click="type = 3">{{ '水友回:' + typelist[3] }}</view>
					<view style="color: #d64700; margin-right: 1.5vh" @click="type = 4">{{ 'DD歌回:' + typelist[4] }}</view>
					<view style="color: #550000; margin-right: 1.5vh" @click="type = 5">{{ '联动回:' + typelist[5] }}</view>
					<view style="color: #b67900; margin-right: 1.5vh" @click="type = 6">{{ '二创回:' + typelist[6] }}</view>
					<view style="color: #069e8c; margin-right: 1.5vh" @click="type = 7">{{ '其他:' + typelist[7] }}</view>
					<view style="margin-left: auto" :style="{ color: gettype1(0) }">{{ '2025/09/01 - 至今' }}</view>
					<view style="margin-right: 0px; margin-left: 1.5vh" :style="{ color: gettype1(0) }">{{ '直播分类:' + gettype(this.type) }}</view>
				</view>
				<view
					style="width: 13.5%; height: 11vh; border-radius: 0px; position: relative; background-color: rgba(255, 255, 255, 1)"
					:style="{
						marginRight: isLiving && item.frame == true ? '-3px' : '0',
						marginTop: isLiving && item.frame == true ? '2px' : '5px',
						marginBottom: isLiving && item.frame == true ? '2px' : '5px',
						color: getcolor1(item.status, item.type),
						border: !isLiving && item.frame == true ? '2px solid ' + getcolor1(item.status, item.type) : '',
					}"
					v-for="(item, index) in list"
					@click="linkto(item.url)"
					:class="{ 'flow-border': isLiving && item.frame == true, item: !(isLiving && item.frame == true) }"
					v-if="type == -1 || type == item.type || (typeof item.type == 'string' && item.type.indexOf(type) != -1)"
				>
					<view style="width: 100%; height: 100%; position: relative; overflow: hidden; z-index: 2; background-color: white">
						<view style="width: 95%; height: 95%; padding: 2.5%; display: flex; flex-direction: column; z-index: 9; position: relative">
							<text style="font-size: 1.5vh; margin-bottom: 2px" v-if="item.time == null">{{ item.date + '/' + item.week }}</text>
							<view style="display: flex; flex-direction: row; align-items: center; justify-content: space-between" v-else>
								<text style="font-size: 1.5vh; margin-bottom: 2px" :style="{ marginTop: juge2(item.type) ? '-0.65vh' : '0px' }">
									{{ item.date + '/' + item.week }}
								</text>
								<view style="font-size: 1.3vh; margin-bottom: 2px; display: flex; flex-direction: row; align-items: end" v-if="item.frame == true && isLiving">
									<view class="play-bar-1" style="width: 7px" :style="{ backgroundColor: getcolor1(item.status, item.type) }"></view>
									<view
										class="play-bar-2"
										style="width: 7px; margin-left: 1px; margin-right: 1px"
										:style="{ backgroundColor: getcolor1(item.status, item.type) }"
									></view>
									<view class="play-bar-3" style="width: 7px; margin-right: 5px" :style="{ backgroundColor: getcolor1(item.status, item.type) }"></view>

									<text>{{ '直播中' }}</text>
								</view>
								<text style="font-size: 1.3vh; margin-bottom: 2px" v-else>{{ item.time }}</text>
							</view>
							<text v-if="item.status == 1" style="font-size: 1.8vh" :style="{ marginTop: juge2(item.type) ? '-0.65vh' : '0vh' }">
								{{ item.title == null ? gettype(item.type) : item.title }}
							</text>
							<text v-if="item.status == 0" style="font-size: 1.8vh">{{ '休息日' }}</text>
							<text v-if="item.status == -1" style="font-size: 1.8vh">{{ '待定' }}</text>
							<text v-if="item.status == 1" style="font-size: 1.6vh">{{ item.data }}</text>
						</view>
						<view
							style="width: 100%; height: 100%; position: absolute; z-index: 2; top: 0; left: 0; opacity: 0.8"
							:style="{ background: getcolor(item.status, item.type) }"
						></view>
						<view
							style="
								width: 100%;
								height: 100%;
								opacity: 0.2;
								position: absolute;
								top: 0;
								left: 0;
								z-index: 1;
								display: flex;
								align-items: center;
								justify-content: center;
								overflow: hidden;
							"
						>
							<view v-if="juge2(item.type) && item.image.indexOf(';') != -1" style="width: 100%; height: 100%; position: relative; overflow: hidden">
								<!-- 左半部分梯形图片 -->
								<image
									style="width: 100%;height: 100%;position: absolute;2;
						               clip-path: polygon(0 0, 100% 0, 50% 100%, 0 100%);"
									:mode="'aspectFill'"
									:src="item.image.split(';')[0]"
								></image>
								<!-- 右半部分梯形图片 -->
								<image
									style="width: 70%;height: 100%;position: absolute;1;right:0;
						               clip-path: polygon(50% 0, 100% 0, 100% 100%, 0 100%);"
									:mode="'aspectFill'"
									:src="item.image.split(';')[1]"
								></image>
							</view>

							<image
								v-else
								style="width: 100%; height: 150%"
								:mode="item.type == 6 ? 'widthFix' : item.status == 0 ? 'heightFix' : 'aspectFill'"
								:src="getimage(item)"
							></image>
						</view>
					</view>
				</view>
				<view style="width: 13.5%; height: 11vh; border-radius: 0px; position: relative" v-for="i in juge1()" v-if="type != -1 && 7 - (typelist[type] % 7) != 7"></view>
			</view>
		</u-transition>
	</view>
</template>

<script>
export default {
	data() {
		return {
			type: -1,
			num: 0,
			isLiving: false,
			list: [],
			typelist: [0, 0, 0, 0, 0, 0, 0, 0],
			//type 0:杂谈 1:歌回 2:游戏回 3:水友回 4:DD歌回 5:联动回 6:二创回 7:其他
			date: [],
			show1: false,
		}
	},
	methods: {
		juge2(e) {
			if (typeof e == 'string') {
				if (e.indexOf(',') != -1) return true
				return false
			} else return false
		},
		juge1() {
			if (this.type == -1) return 0

			return 7 - (this.typelist[this.type] % 7)
		},
		gettype1(e) {
			e = JSON.parse(JSON.stringify(e))
			if (this.type == -1) return '#6e5bd8'
			if (this.type == 0) return '#9e2d73'
			if (this.type == 1) return '#7400da'
			if (this.type == 2) return '#326699'
			if (this.type == 3) return '#287a7a'
			if (this.type == 4) return '#d64700'
			if (this.type == 5) return '#550000'
			if (this.type == 6) return '#b67900'
			if (this.type == 7) return '#069e8c'
		},
		close() {
			this.show1 = false
		},
		linkto(e) {
			if (e == null) window.open('https://live.bilibili.com/2058234')
			else window.open(e)
		},
		getimage(e) {
			e = JSON.parse(JSON.stringify(e))
			if (e.image != null && e.image != '') return e.image
			if (typeof e.type == 'string') {
				e.type = parseInt(e.type.split(',')[0])
			}
			if (e.status == -1) return 'https://image.begonia.cafe/tx/new/wait.webp'
			if (e.status == 0) return 'https://image.begonia.cafe/tx/new/sleep.webp'
			if (e.type == 0) return 'https://image.begonia.cafe/tx/new/CBAE07F605E0676868DD7E3F12202F7E.jpg'
			if (e.type == 1) return 'https://image.begonia.cafe/tx/new/image6.webp'
			if (e.type == 4) return 'https://image.begonia.cafe/tx/new/image4.webp'
			if (e.type == 5) return 'https://image.begonia.cafe/tx/new/image5.webp'
			if (e.type == 6) return '/static/title.webp'
			return e.image
		},
		gettype(e) {
			e = JSON.parse(JSON.stringify(e))
			//type 0:杂谈 1:歌回 2:游戏回 3:水友回 4:DD歌回 5:联动回 6:二创回 7:其他
			if (typeof e == 'string') {
				e = parseInt(e.split(',')[0])
			}
			if (e == -1) return '全部'
			if (e == 0) return '杂谈'
			if (e == 1) return '歌回'
			if (e == 2) return '游戏回'
			if (e == 3) return '水友回'
			if (e == 4) return 'DD歌回'
			if (e == 5) return '联动回'
			if (e == 6) return '二创回'
			if (e == 7) return '其他'
		},
		getcolor(i, e) {
			e = JSON.parse(JSON.stringify(e))
			if (typeof e == 'string') {
				e = parseInt(e.split(',')[0])
			}
			if (i == 0) return 'linear-gradient(to right,rgba(177, 171, 255, 0.4),rgba(177, 171, 255, 0.05))'
			if (i == -1) return 'linear-gradient(to right,rgba(239,239,239,0.8),rgba(239,239,239,0.8))'
			if (e == 0) return 'linear-gradient(to right,rgba(255, 170, 255, 0.4),rgba(255, 170, 255, 0.05)'
			if (e == 1) return 'linear-gradient(to right,rgba(166, 57, 255, 0.4),rgba(166, 57, 255, 0.05))'
			if (e == 2) return 'linear-gradient(to right,rgba(85,170,255,0.4),rgba(85,170,255,0.05))'
			if (e == 3) return 'linear-gradient(to right,rgba(85,255,255,0.4),rgba(85,255,255,0.05))'
			if (e == 4) return 'linear-gradient(to right,rgba(255,85,0,0.4),rgba(255,85,0,0.05))'
			if (e == 5) return 'linear-gradient(to right,rgba(139, 0, 0, 0.4),rgba(139, 0, 0, 0.05))'
			if (e == 6) return 'linear-gradient(to right,rgba(255, 170, 0, 0.4),rgba(255, 170, 0, 0.05))'
			if (e == 7) return 'linear-gradient(to right,rgba(107, 212, 200, 0.4),rgba(107, 212, 200, 0.05))'
		},
		getcolor1(i, e) {
			e = JSON.parse(JSON.stringify(e))
			if (typeof e == 'string') {
				e = parseInt(e.split(',')[0])
			}
			if (i == -1) return '#606266'
			if (i == 0) return '#6e5bd8'
			if (e == 0) return '#9e2d73'
			if (e == 1) return '#7400da'
			if (e == 2) return '#326699'
			if (e == 3) return '#287a7a'
			if (e == 4) return '#d64700'
			if (e == 5) return '#550000'
			if (e == 6) return '#b67900'
			if (e == 7) return '#069e8c'
		},
		generateCurrentMonthDates() {
			const dateArray = []
			const today = new Date()
			today.setHours(0, 0, 0, 0) // 清除时间部分，仅保留日期

			// ===================== 1. 确定关键时间点 =====================
			// 固定起始日期：2025年9月1日（月份0-11，故9月用8表示）
			const startDate = new Date(2025, 8, 1)
			startDate.setHours(0, 0, 0, 0)

			// 本周的周末（周日）：延续原逻辑（周一到周日为一周）
			const weekStart = new Date(today)
			const weekDay = today.getDay() || 7 // 周日的getDay()为0，转为7
			weekStart.setDate(today.getDate() - (weekDay - 1)) // 本周一
			weekStart.setHours(0, 0, 0, 0)
			const weekEnd = new Date(weekStart)
			weekEnd.setDate(weekStart.getDate() + 6) // 本周日（周末）
			weekEnd.setHours(23, 59, 59, 999) // 周末当天的结束时间

			// 边界处理：若起始日期晚于周末（理论上2025/09后使用，暂提示兼容）
			if (startDate > weekEnd) {
				return dateArray
			}

			// ===================== 2. 生成日期数组（2025/09/01 至 本周日） =====================
			const weekMap = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六']
			let currentDate = new Date(startDate) // 从起始日期开始遍历

			while (currentDate <= weekEnd) {
				// 计算日期状态：大于今天且不在本周内 → status=-1（不可选），否则0（可选）
				let status = 0
				if (currentDate >= today) {
					if (currentDate >= weekStart && currentDate <= weekEnd) {
						status = -1
					}
				}

				// 格式化日期（两位数年份/月份/日期）
				const year = currentDate.getFullYear()
				const shortYear = String(year).slice(-2)
				const formattedMonth = String(currentDate.getMonth() + 1).padStart(2, '0')
				const formattedDay = String(currentDate.getDate()).padStart(2, '0')

				// 组装日期对象（保留原结构）
				const dateItem = {
					date: `${shortYear}/${formattedMonth}/${formattedDay}`,
					week: weekMap[currentDate.getDay()], // 对应中文星期
					status: status,
					type: -1,
					data: '',
					frame: currentDate.getFullYear() === today.getFullYear() && currentDate.getMonth() === today.getMonth() && currentDate.getDate() === today.getDate(), // 当天日期标红/高亮标识
				}

				dateArray.push(dateItem)
				// 日期+1，继续遍历下一天
				currentDate.setDate(currentDate.getDate() + 1)
			}

			// ===================== 3. 数组倒序（从本周周末倒推至2025/09/01） =====================
			dateArray.reverse()

			return dateArray
		},
		juge(y, m, d) {
			var date = y
			if (m < 10) date += '/0' + m
			else date += '/' + m
			if (d < 10) date += '/0' + d
			else date += '/' + d
			return date
		},
	},
	mounted() {
		var uid = 703405
		//var uid = 1639389144
		uni.request({
			url: '/api/getbilibiliroom?uid=' + uid,
			method: 'GET',
			success: (res) => {
				this.isLiving = res.data.data.channel.isLiving
			},
			fail: () => {},
		})
		this.list = this.generateCurrentMonthDates()
		uni.request({
			url: '/api/getdate',
			method: 'POST',
			data: {},
			success: (res) => {
				this.date = res.data.data
				for (var x = 0; x < this.date.length; x++) {
					for (var y = 0; y < this.list.length; y++)
						if (this.juge(this.date[x].y, this.date[x].m, this.date[x].d) == this.list[y].date) {
							this.list[y].status = this.date[x].status
							this.list[y].type = this.date[x].type
							this.list[y].data = this.date[x].data
							this.list[y].image = this.date[x].image
							this.list[y].time = this.date[x].time
							this.list[y].url = this.date[x].url
							this.list[y].title = this.date[x].title
							var juge = this.date[x].type + ''
							if (this.date[x].status == 0 || this.date[x].status == -1) {
								this.list[y].type = -1
								continue
							}
							if (juge.indexOf(',') != -1) {
								var data = this.date[x].type.split(',')
								data = [...new Set(data)]
								console.log(data)
								for (var z = 0; z < data.length; z++) {
									this.typelist[data[z]]++
								}
							} else {
								this.typelist[this.date[x].type]++
								if (this.date[x].type == '0') console.log(this.date[x])
							}
						}
				}
				for (var x = 0; x < this.typelist.length; x++) {
					this.num += this.typelist[x]
				}
				this.show1 = true
			},
		})
	},
}
</script>

<style>
.item:hover {
	transform: scale(1.1);
}
.item {
	transition: 0.5s;
}
.flow-border:hover {
	transform: scale(1.1);
}
.flow-border {
	transition: 0.5s;
	padding: 3px;
	display: flex;
	align-items: center;
	justify-content: center;
	color: #333;

	/* 核心：渐变首尾颜色一致，确保循环衔接 */
	background: linear-gradient(90deg, #ff784f, /* 起始色 */ #ffd467, #86ccb8, #3ec86c, #4759ff, #da6bff /* 结束色（与起始色相同） */);

	background-clip: border-box;
	-webkit-background-clip: border-box;
	background-size: 200% 100%; /* 横向拉伸4倍，预留足够动画空间 */

	/* 明确指定无限循环 + 匀速动画 */
	animation: flow 2s linear infinite;
	animation-direction: alternate;
	animation-iteration-count: infinite; /* 显式声明无限循环（默认可省略） */
}

/* 关键：动画结束状态与开始状态完全衔接 */
@keyframes flow {
	0% {
		background-position: 0% 0%; /* 开始位置 */
	}
	100% {
		background-position: 100% 0%; /* 结束位置（与开始位置形成闭环） */
	}
}
/* 第一个方块：中等高度波动，延迟0ms */
.play-bar-1 {
	/* 初始高度 */
	height: 5px;
	/* 动画：高度变化+循环 */
	animation: barWave1 1s ease-in-out infinite;
}

/* 第二个方块：偏低高度波动，延迟100ms */
.play-bar-2 {
	height: 2px;
	animation: barWave2 0.5s ease-in-out infinite;
	animation-delay: 100ms; /* 与第一个方块错开节奏 */
}

/* 第三个方块：偏高高度波动，延迟200ms */
.play-bar-3 {
	height: 7px;
	animation: barWave3 0.8s ease-in-out infinite;
	animation-delay: 200ms; /* 与前两个方块形成错落感 */
}

/* 第一个方块动画关键帧 */
@keyframes barWave1 {
	0%,
	100% {
		height: 5px;
	} /* 起始和结束高度 */
	50% {
		height: 10px;
	} /* 中间最高高度 */
}

/* 第二个方块动画关键帧 */
@keyframes barWave2 {
	0%,
	100% {
		height: 2px;
	}
	50% {
		height: 8px;
	} /* 比第一个略低 */
}

/* 第三个方块动画关键帧 */
@keyframes barWave3 {
	0%,
	100% {
		height: 7px;
	}
	50% {
		height: 15px;
	} /* 三个中最高 */
}
</style>
