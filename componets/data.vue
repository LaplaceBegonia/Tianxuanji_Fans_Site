<template>
	<view style="width:100%;height:100%">
		<u-transition  mode="fade" :show="!show"
		style="width: 100%;height: 100%;display: flex;align-items: center;justify-content: center;font-size: 8vh;color:aqua"
		>
			 <div class="loading-container">
			        <!-- 环形Loading -->
			        <div class="magic-loading" style="position: relative;">
						
					</div>
			        <!-- 加载提示文字 -->
			        <div class="loading-text">加载中...</div>
			    </div>
		</u-transition>
		<u-transition  mode="fade" :show="show&&data.channel==null"
		style="width: 100%;height: 100%;display: flex;align-items: center;font-size: 8vh;"
		>	
			<view style="width: 100%;height: 100%;overflow-y: auto;padding-top:10vh;padding-bottom: 10vh;display: flex;flex-direction: column;align-items: center;" >
			<view style="font-size: 4vh;font-style: italic;margin-bottom: 2vh;margin-top: -1vh;">{{"直播数据"}}</view>
			<view style="width: 80vw;display: flex;flex-direction: row;align-items: center;background-color: rgba(255,255,255,0.5);padding:1vh;font-size: 2vh;justify-content: space-around;margin-top: 2vh;" >
				{{"Danmakus接口错误，请等待服务恢复"}}
			</view>
			</view>
		</u-transition>
		<u-transition mode="fade" :show="show&&data.channel!=null"
		style="width: 100%;height: 100%;"
		>
			<view style="width: 100%;height: 100%;overflow-y: auto;padding-top:10vh;padding-bottom: 10vh;display: flex;flex-direction: column;align-items: center;" v-if="show">
				<view style=" font-family: 'Orbitron', sans-serif;
				font-size: 4vh;
				font-weight: 800;
				margin-bottom: 2vh;
				margin-top: 0vh;
				color: #3c9cff;
				text-shadow: 0 0 10px rgba(60, 156, 255, 0.3)">{{"直播数据"}}</view>
				<view style="border-radius: 10px 10px 0 0;box-shadow: 0 0 15px rgba(193, 229, 255, 0.8);width: 80vw;display: flex;flex-direction: row;align-items: center;background-color: rgba(255,255,255,0.5);padding:1vh;font-size: 2vh;justify-content: space-around;margin-top: 2vh;" >
					<view style="display: flex;flex-direction: column;" >
						<text>{{data.channel.uName}}</text>
						<text>{{"房间号:"+data.channel.roomId}}</text>
					</view>
					<view style="display: flex;flex-direction: column;" >
						<text>{{"直播总场次:"+data.channel.totalLiveCount}}</text>
						<text>{{"直播总时长:"+formatDuration(data.channel.totalLiveSecond)}}</text>
					</view>
					<view style="display: flex;flex-direction: column;" >
						<text>{{"场均流水:¥"+(money/num).toFixed(2)}}</text>
						<text>{{"总流水:¥"+money}}</text>
					</view>
					<view style="display: flex;flex-direction: column;" >
						<text>{{"当前直播状态:"+(data.channel.isLiving==true?'直播中':'未直播')}}</text>
						<text>{{"总弹幕:"+data.channel.totalDanmakuCount}}</text>
					</view>
				</view>
				<view style="box-shadow: 0 0 15px rgba(193, 229, 255, 0.8);width: 80vw;display: flex;flex-direction: row;align-items: center;background-color: rgba(255,255,255,0.5);padding:1vh;font-size: 2vh;justify-content: space-around;margin-top: 2vh;flex-wrap: wrap;
				padding-top: 2vh;padding-bottom: 2vh
				" >	
					<view class="charts-box" style="width: 100%;">
					    <qiun-data-charts 
							type="line"
							:opts="opts"
							:chartData="chartData"
					    />
					</view>
				</view>
				<view style="box-shadow: 0 0 15px rgba(193, 229, 255, 0.8);width: 80vw;display: flex;flex-direction: row;align-items: center;background-color: rgba(255,255,255,0.5);padding:1vh;font-size: 2vh;justify-content: space-around;margin-top: 2vh;flex-wrap: wrap;
				padding-top: 2vh;padding-bottom: 2vh;border-radius: 0 0 10px 10px;
				" >
					<view style="width: 30%;height: 10rem;margin-bottom: 20px;display: flex;flex-direction: row;align-items: center;padding-top: 0px;padding-bottom: 20px "
					v-for="(item,index) in data.lives"  
					:class="{ visible: show }"
					:style="{ transitionDelay: `${index * 0.2}s` }"
					@click="openpage('https://live.bilibili.com/2058234')"
					>
						<img referrerpolicy="no-referrer"  :src="item.coverUrl" style="height: 16vh;width:auto;border-radius: 5px;margin-right: 10px;" mode="heightFix"></img>
						<view style="height: 16vh;width: auto;display: flex;flex-direction: column">
							<text style="font-size: 1.8vh;">{{item.title}}</text>
							<text style="font-size: 1.65vh;">{{getdate(item.startDate)+" "+getxingqi(item.startDate)}}</text>
							<text style="font-size: 1.65vh;">{{gettime(item.startDate)+" - "+gettime(item.stopDate)}}</text>
							<text style="font-size: 1.5vh;">{{"观看量:"+item.watchCount}}</text>	
							<text style="font-size: 1.5vh;">{{"弹幕:"+item.danmakusCount}}</text>	
							<text style="font-size: 1.5vh;">{{"流水:¥"+item.totalIncome}}</text>	
						</view>
					</view>
					<view style="width: 30%;height: 16vh;margin-bottom: 20px;display: flex;flex-direction: row;align-items: center;padding-top: 0px;padding-bottom: 20px "
					v-for="(item,index) in 3-data.lives.length%3" v-if='(data.lives.length%3)!=0'></view>
				</view>
			</view>
		</u-transition>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				data:{},
				show:false,
				money:0.0,
				num:0,
				opts: {
				    color: ["#1890FF","#EE6666","#ffaa00","#00ffff","#ff00ff"],
				    padding: [15,10,0,15],
				    enableScroll: false,
					dataPointShape: false,
					dataLabel:false,
				    legend: {
						show:true
					},
				    xAxis: {
				        disableGrid: true,
						labelCount:0,
						disabled:true,
						boundaryGap:"justify"
				    },
				    yAxis: {
				        gridType: "dash",
				        dashLength: 2,
						disabled:true
				    },
				    extra: {
						showBox:true,
				        line: {
							type: "curve",
				            width: 2.5,
				            activeType: "none",
							
				        },
						tooltip:{
							legendShape:"auto",
							gridType:"dash"
						}
				    }
				},
				chartData: {},
			}
		},
		methods: {
			close(){
				this.show=false;
			},
			openpage(e){
				window.open(e)
			},
			formatDuration(timestamp) {
			    // 确保输入是数字类型
			    const totalSeconds = parseInt(timestamp);
			    
			    // 计算小时、分钟和剩余秒数
			    const hours = Math.floor(totalSeconds / 3600);
			    const minutes = Math.floor((totalSeconds % 3600) / 60);
			    const seconds = totalSeconds % 60;
			    
			    // 格式化为两位数字符串 (00:00:00)
			    const pad = (num) => num.toString().padStart(2, '0');
			    
			    return `${pad(hours)}:${pad(minutes)}:${pad(seconds)}`;
			},
			getdate(timestamp){
				const date = new Date(timestamp); 
				const year = date.getFullYear();
				const month = String(date.getMonth() + 1).padStart(2, '0'); // 月份从0开始
				const day = String(date.getDate()).padStart(2, '0');
				    
				return `${year}-${month}-${day}`;
			},
			gettime(timestamp){
				 const date = new Date(timestamp);
				    
				const hours = String(date.getHours()).padStart(2, '0');
				const minutes = String(date.getMinutes()).padStart(2, '0');
				const seconds = String(date.getSeconds()).padStart(2, '0');
				    
				return `${hours}:${minutes}:${seconds}`;
			},
			getxingqi(timestamp){
				const days = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
				return days[new Date(timestamp).getDay()];
			},
			getDuration(startDate, stopDate) {
			    // 确保输入转换为Date对象
			    const start = new Date(startDate);
			    const stop = new Date(stopDate);
			    
			    // 计算时间差（毫秒）
			    const diffMs = stop - start;
			    
			    // 处理无效日期或结束时间早于开始时间的情况
			    if (isNaN(diffMs) || diffMs < 0) {
			        return "0h0m";
			    }
			    
			    // 计算小时和分钟
			    const diffMinutes = Math.floor(diffMs / (1000 * 60));
			    const hours = Math.floor(diffMinutes / 60);
			    const minutes = diffMinutes % 60;
			    
			    return `${hours}h ${minutes}m`;
			},
		},
		mounted(){
			var uid = 703405
			//var uid = 3494357252442916
			uni.request({
				url:"/api/getbilibiliroom?uid="+uid,
				method:"GET",
				success: (res) => {
					try{
						this.data=res.data.data
						res={
							categories:[],
							series:[
								{
									name:"",
									data:[]
								},
								{
									name:"",
									data:[]
								},
								{
									name:"",
									data:[]
								},
								{
									name:"",
									data:[]
								},
								{
									name:"",
									data:[]
								}
							]
						}
						var temp = 0
						for(var x=0;x<this.data.lives.length;x++){
							this.money+=this.data.lives[x].totalIncome
							if(this.data.lives[x].startDate>1735660800){
								var time = this.data.lives[x].stopDate-this.data.lives[x].startDate
								temp+=time
							}
							if(this.data.lives[x].totalIncome>0){
								this.num++
								res.categories.unshift(this.getdate(this.data.lives[x].startDate))
								res.series[0].name='流水'
								res.series[1].name='观看'
								res.series[2].name='互动'
								res.series[3].name='弹幕'
								res.series[4].name='人均弹幕'
								res.series[0].data.unshift(this.data.lives[x].totalIncome)
								res.series[1].data.unshift(this.data.lives[x].watchCount)
								res.series[2].data.unshift(this.data.lives[x].interactionCount)
								res.series[3].data.unshift(this.data.lives[x].danmakusCount)
								res.series[4].data.unshift(parseInt(this.data.lives[x].danmakusCount/this.data.lives[x].interactionCount))
							}
						}
						//console.log(temp)
						this.chartData = JSON.parse(JSON.stringify(res));
						this.money=this.money.toFixed(2)
						this.show=true;
					}catch(e){
						this.data={
							channel:null
						}
						this.show=true;
					}	
				},
				fail: () => {
					this.show=true;
				}
			})
		}
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
            border-top-color: #5DE6DC; /* 主题青色 */
            border-right-color: #A78BFA; /* 辅助紫色 */
            border-bottom-color: #5DE6DC;
            border-left-color: #A78BFA;
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
            background-color: #5DE6DC;
            box-shadow: 0 0 10px rgba(93, 230, 220, 0.8); /* 发光效果 */
        }

        /* 加载文字提示 */
        .loading-text {
            margin-top: 20px;
            font-size: 18px;
            color: #3BC8BE; /* 深色主题青 */
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
