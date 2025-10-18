<template>
	<view style="width:2048px;height: 100vh;position: relative;overflow-y: hidden;background-repeat:no-repeat;
    background-attachment:fixed;color:rgb(96, 98, 102);transform-origin:left top; height: 100vh;
    background-position:center;background-size:cover;" :style="{width:type==0?(vw1+'px'):'100vw'}" class="main-container">
		<image src="https://image.begonia.cafe/tx/bg1.webp" style="width: 100vw;height: 100%;position: fixed;z-index: -1;" mode="aspectFill" v-show="type==1"
		:class="{'op2':bg==1}"
		></image>
		<image src="https://image.begonia.cafe/tx/bg2.webp" style="width:100vw ;height: 100vh;position: fixed;z-index: -1;transition: 0.5s;" mode="aspectFill" v-show="type==0&&!bg4"
		:class="{'op2':bg==2,'op1':bg!=2}"
		></image>
		<image src="https://image.begonia.cafe/tx/bg3.webp" style="width: 100vw;height: 100vh;position: fixed;z-index: -1;transition: 0.5s;" mode="aspectFill" v-show="type==0&&!bg4"
		:class="{'op2':bg==3,'op1':bg!=3}"
		></image>
		<image src="https://image.begonia.cafe/tx/bg.webp" style="width: 100vw;height: 100vh;position: fixed;z-index: -1;transition: 0.5s;" mode="aspectFill"v-show="type==0&&!bg4"
		:class="{'op2':bg==1,'op1':bg!=1}"
		></image>
		<image src="https://image.begonia.cafe/tx/00027.webp" style="width:100vw ;height: 100vh;position: fixed;z-index: -1;transition: 0.5s;" mode="aspectFill" v-show="type==0&&bg4"
		:class="{'op2':bg==2,'op1':bg!=2}"
		></image>
		<image src="https://image.begonia.cafe/tx/00009-4020265700.webp" style="width: 100vw;height: 100vh;position: fixed;z-index: -1;transition: 0.5s;" mode="aspectFill" v-show="type==0&&bg4"
		:class="{'op2':bg==3,'op1':bg!=3}"
		></image>
		<image src="https://image.begonia.cafe/tx/00166.webp" style="width: 100vw;height: 100vh;position: fixed;z-index: -1;transition: 0.5s;" mode="aspectFill"v-show="type==0&&bg4"
		:class="{'op2':bg==1,'op1':bg!=1}"
		></image>
		<image src="/static/doro.gif" style="height: 120px;width: 100px;position: fixed;z-index: 0;bottom:10px;" mode="heightFix"
		:class="{'right':!show7,'left':show7}" v-if="type==0"
		></image>
		<image src="/static/doro1.gif" style="height: 120px;width: 100px;position: fixed;z-index: 0;bottom:10px;" mode="heightFix"
		:class="{'right':!show10,'left1':show10}" v-if="type==0"
		></image>
		<image src="/static/doro2.gif" style="height: 120px;width: 100px;position: fixed;z-index: 0;bottom:10px;" mode="heightFix"
		:class="{'right':!show11,'left2':show11}" v-if="type==0"
		></image>
		<view style="width: 12vh;height: 12vh;display: flex;align-items: flex-end;justify-content: center;background-color: rgba(164,255,255,0.8);color:white;
		position:fixed;top:-6vh;right:-6vh;transform: rotate(45deg);font-size: 2vh;" @click="showinfo=true" v-if="type==0">  
			日程表
		</view>
		<view style="width: 12vh;height: 12vh;display: flex;align-items: flex-end;justify-content: center;background-color: rgba(164,255,255,0.8);color:white;
		position:fixed;top:-6vh;left:-6vh;transform: rotate(-45deg);font-size: 2vh;" @click="linkto1('/pages/new/new')" v-if="type==0">  
			新版测试
		</view>
		<!--音乐-->
		<view style="display: flex;flex-direction: row;align-items: center;width: 23.8 vw;position: fixed;top:15vh;z-index: 99;height: 10vh;transition: 1s;"
		:style="{left:musicshow?'0':'-21vw'}" v-if="type==0"
		>
			<view style="height: 22vh;border-radius: 0px 10px 10px 0px;width: 21vw;display: flex;flex-direction: row;align-items: center;margin-top: 20px;" 		:style="{backgroundColor:color}">
				<view style="width: 20vw;height: 19.5vh;background-color: rgba(255,255,255,0.7);border-radius:0px 5px 5px 0px;display: flex;flex-direction: row;align-items: center;">
					<image :class="{'rotate-animation':isplay}" :src="musiclist[musicindex].cover" style="height: 10vh;width: 10vh;border-radius: 50%;border:10px solid rgba(164,255,255,0.8);margin-left: 5px;"></image>
					<view style='width: 12vw;height: 90%;margin-top:0%;background-color:rgba(255,255,255,0.3);border-radius:5px;margin-left: 15px;display: flex;flex-direction: column;align-items: center;justify-content:center;'>
						<text style="font-size: 1.8vh;color:black;font-weight: 700;font-style: italic;">{{musiclist[musicindex].name}}</text>
						<view style="font-size: 1.5vh;color:white;height: 6vh;margin-top: 5px;margin-bottom: 5px;display: flex;align-items: center;justify-content: center;">
							<scroll-view
								style="height: 6vh;"
								class="lyric-scroll" 
								scroll-y scroll-with-animation
								:scroll-top="scrollTop"
							>
							  <view 
							    v-for="(line, index) in lyricList" 
							    :key="index" 
								style="font-size: 1.3vh"
							    class="lyric-line"
							    :class="{ 'active': currentLyricIndex === index,'unactive1':currentLyricIndex != index  && !bg4 ,'unactive2':currentLyricIndex != index  && bg4 }"
			
							  >
							    <text :title="line.text">{{ (line.text.indexOf('（')!=-1&&line.text.length>20)?(line.text.substring(0,14)+".."):line.text }}</text>
							  </view>
							</scroll-view>
						</view>
						<view style="height:2vh;display: flex;align-items: center;justify-content: center;width: 100%;margin-top: 5px;margin-bottom: 5px">
							<progres :progress='progress' :totalTime="0" @progress-change="progresschange" ></progres>	
						</view>
						
						<view style="display: flex;flex-direction: row;align-items: center;width: 100%;justify-content: space-around;">
							<u-icon name="rewind-left-fill" size="2.5vh" color="#5555ff" @click="last"></u-icon>
							<u-icon name="rewind-right-fill"size="2.5vh"  color="#5555ff" @click="next"></u-icon>
							<u-icon name="pause-circle-fill"size="2.5vh" @click="musicstop" v-if="isplay" color="#5555ff"></u-icon>
							<u-icon name="play-circle-fill" size="2.5vh" @click="musicplay" v-else color="#5555ff"></u-icon>
							<u-icon name="volume-fill" size="2.5vh"  v-if="noise" @click="stopnoise" color="#5555ff"></u-icon>
							<u-icon name="volume-off-fill" size="2.5vh"  v-else @click="opennoise" color="#5555ff"></u-icon>
						</view>
					</view>
					
				</view>
			</view>
			<view style="width: 1.8vw;height: 1.8vw;border-radius: 0px 10px 10px 0px;display: flex;flex-direction: row;align-items: center;justify-content: center;":style="{backgroundColor:color}"
			@click="musicshow=!musicshow"
			>
				<u-icon :name="musicshow?'arrow-down-fill':'arrow-up-fill'" style="transform: rotate(90deg);transition: 1s;":color="bg4?'rgba(255,255,255,0.7)':'rgb(96,98,102)'"  size="2vh"></u-icon>
			</view>
		</view>
		<!--顶部导航栏-->
		<view style="height:5vh;border-radius: 0px 0px 10px 10px;
		display: flex;flex-direction: row;align-items: center;justify-content: space-around;;font-size: 1rem;transition: 0.1s;
		" :class="{'top1':show==false,'top2':show==true}" :style="{width:type==0?(margin*0.4)+'px':'100%',backgroundColor:color,marginLeft:(margin*0.3)+'px',marginRight:(margin*0.3)+'px'}"
		>	
			<view style="display: flex;flex-direction: column;align-items: center;justify-content: center;" @click="page=0">
				<u-icon name="calendar" :size="'3vh'" :color="bg4?'rgba(255,255,255,0.7)':'rgb(96,98,102)'"></u-icon>
				<view style="margin-left: 0.5rem;margin-right: 1vh;font-size: 1.5vh;":style="{color:bg4?'rgba(255,255,255,0.7)':'rgb(96,98,102)'}">
				周表
				</view>
			</view>
			<view style="display: flex;flex-direction: column;align-items: center;justify-content: center;" @click="page=1">
				<u-icon name="clock-fill" :size="'3vh'" :color="bg4?'rgba(255,255,255,0.7)':'rgb(96,98,102)'"></u-icon>
				<view style="margin-top: -2px;font-size: 1.5vh;":style="{color:bg4?'rgba(255,255,255,0.7)':'rgb(96,98,102)'}">数据</view>
			</view>
			<view style="display: flex;flex-direction: column;align-items: center;justify-content: center;" @click="page=2">
				<u-icon name="cut" :size="'3vh'" :color="bg4?'rgba(255,255,255,0.7)':'rgb(96,98,102)'"></u-icon>
				<view style="margin-top: -2px;font-size: 1.5vh;":style="{color:bg4?'rgba(255,255,255,0.7)':'rgb(96,98,102)'}">切片</view>
			</view>
			<view style="display: flex;flex-direction: column;align-items: center;justify-content: center;" @click="page=8">
				<u-icon name="order" :size="'3vh'" :color="bg4?'rgba(255,255,255,0.7)':'rgb(96,98,102)'"></u-icon>
				<view style="margin-top: -2px;font-size: 1.5vh;":style="{color:bg4?'rgba(255,255,255,0.7)':'rgb(96,98,102)'}">文选</view>
			</view>
			<view style="display: flex;flex-direction: column;align-items: center;justify-content: center;" @click="page=3">
			<u-icon name="tags-fill" :size="'3vh'" style="margin-left: 0px;" :color="bg4?'rgba(255,255,255,0.7)':'rgb(96,98,102)'"></u-icon>
				<view style="margin-top: -2px;font-size: 1.5vh;margin-left: 0px;":style="{color:bg4?'rgba(255,255,255,0.7)':'rgb(96,98,102)'}">关于</view>
			</view>
			<view style="display: flex;flex-direction: column;align-items: center;justify-content: center;" @click="page=5">
			<u-icon name="photo-fill" :size="'3vh'" :color="bg4?'rgba(255,255,255,0.7)':'rgb(96,98,102)'"></u-icon>
				<view style="margin-top: -2px;font-size: 1.5vh;":style="{color:bg4?'rgba(255,255,255,0.7)':'rgb(96,98,102)'}">素材</view>
			</view>
			<view style="display: flex;flex-direction: column;align-items: center;justify-content: center;" @click="page=4">
				<u-icon name="email" :size="'3vh'" :color="bg4?'rgba(255,255,255,0.7)':'rgb(96,98,102)'"></u-icon>
				<view style="margin-top: -2px;font-size: 1.5vh;":style="{color:bg4?'rgba(255,255,255,0.7)':'rgb(96,98,102)'}">留言</view>
			</view>
			<view style="display: flex;flex-direction: column;align-items: center;justify-content: center;" @click="page=6">
			<u-icon name="setting" :size="'3vh'" :color="bg4?'rgba(255,255,255,0.7)':'rgb(96,98,102)'"></u-icon>
				<view style="margin-top: -2px;font-size: 1.5vh;":style="{color:bg4?'rgba(255,255,255,0.7)':'rgb(96,98,102)'}">设置</view>
			</view>
			<view style="display: flex;flex-direction: column;align-items: center;justify-content: center;" @click="page=7">
			<u-icon name="star-fill" :size="'3vh'" :color="bg4?'rgba(255,255,255,0.7)':'rgb(96,98,102)'"></u-icon>
				<view style="margin-top: -2px;font-size: 1.5vh;":style="{color:bg4?'rgba(255,255,255,0.7)':'rgb(96,98,102)'}">星姬天</view>
			</view>
		</view>
		<!--导航栏隐藏/显示按钮-->
		<view style=";border-radius: 0px 0px 10px 10px;transition: 0.1s;
		display: flex;align-items: center;justify-content: center;position: relative
		"
		:style="{backgroundColor:color,marginLeft:(margin*0.4925)+'px',marginRight:(margin*0.4925)+'px',height:(margin*0.015)+'px',width:(margin*0.015)+'px'}"
		:class="{'top2':show==false,'top2':show==true}" @click="(show=!show,first==true?page=3:page=-1,first=false)"
		>
			<u-icon name="arrow-down-fill" :size="margin*0.01" :color="bg4?'rgba(255,255,255,0.7)':'rgb(96,98,102)'" :class="{'xuanzhuan1':show==false,'xuanzhuan2':show==true}" style="transition: 0.5s;"></u-icon>
		</view>
		<!--设置-->
		<u-transition :show="page==6" mode="fade" v-if="sub>=6">
		    <view class="scroll-container" :style="{backgroundColor:color,width:type==0?'40%':'95%',marginLeft:type==0?'auto':'2.5%',marginRight:type==0?'auto':'2.5%'}" style="height: 85vh;border-radius: 10px;margin-top: 20px;overflow-y: auto;display: flex;align-items: center;flex-direction: column;overflow-x: hidden;">
				<view style="width: 90%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.5rem;
				display: flex;align-items: center;justify-content: center;padding-top:5px;padding-bottom:5px
				;">
					<text>{{"设置"}}</text>
				</view>
				<view style="width: 90%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.1rem;
				display: flex;flex-direction:row;align-items:center;padding-top:5px;padding-bottom:5px;
				;">
					<text style="margin-left: 10px;">{{"网站加载动画"}}</text>
					<u-switch style="margin-left: auto;margin-right: 10px"  v-model="setting1" @change="change1"></u-switch>
				</view>
				<view style="width: 90%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.1rem;
				display: flex;flex-direction:row;align-items:center;padding-top:5px;padding-bottom:5px
				;">
					<text style="margin-left: 10px;">{{"音频播放(因浏览器限制，音频需用户交互后播放)"}}</text>
					<u-switch style="margin-left: auto;margin-right: 10px" v-model="setting2" @change="change2"></u-switch>
					
				</view>
				<view style="width: 90%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.1rem;
				display: flex;flex-direction:row;align-items:center;padding-top:5px;padding-bottom:5px
				;"v-if="type==0">
					<text style="margin-left: 10px;">{{"播放器自动弹出"}}</text>
					<u-switch style="margin-left: auto;margin-right: 10px" v-model="musicautoshow" @change="change5"></u-switch>
					
				</view>
				<view style="width: 90%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.1rem;
				display: flex;flex-direction:row;align-items:center;padding-top:5px;padding-bottom:5px
				;" v-if="type==0">
					<text style="margin-left: 10px;">{{"壁纸切换"}}</text>
					<view style="display: flex;align-items: center;justify-self: center;padding:5px 10px 5px 10px;margin-left:auto;margin-right:10px;border-radius: 5px;color:white;transition: 0.5s;"
					@click="change4" :style="{backgroundColor:fontcolor}"
					>
						切换
					</view>
				</view>
				<view style="width: 90%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.1rem;
				display: flex;flex-direction:row;align-items:center;padding-top:5px;padding-bottom:5px
				;" v-if="show8&&type==0">
					<text style="margin-left: 10px;">{{"doro璇出现概率"}}</text>
					<text style="margin-left: auto;">{{"0%"}}</text>
					<u-slider style="width: 30%;margin-left: 10px;margin-right: 10px;" v-model="showdorosub" :max="100" :min="0" @change="changeshowdoro"></u-slider>
					<text style="margin-right: 10px;">{{"100%"}}</text>
				</view>
				<view style="width: 90%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.1rem;
				display: flex;flex-direction:row;align-items:center;padding-top:5px;padding-bottom:5px
				;" v-if="show8&&type==0">
					<text style="margin-left: 10px;" v-if="showdorosub>0">{{"doro璇去给你买了百事可乐和可口可乐,快说谢谢doro璇"}}</text>
					<text style="margin-left: 10px;" v-if="showdorosub==0">{{"doro璇不理你了"}}</text>
				</view>
				<view style="width: 90%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.2rem;
				display: flex;align-items: center;justify-content: center;padding-top:5px;padding-bottom:5px
				;" >
					<text>{{"天选姬语音列表"}}</text>
				</view>
				<view style="width: 90%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.1rem;
				display: flex;flex-direction:row;align-items:center;padding-top:5px;padding-bottom:5px
				;" v-for="(item,index) in soundlist.normal" >
					<text style="margin-left: 10px;">{{item.name}}</text>
					<u-icon style="margin-left: auto;margin-right: 10px"  name="play-circle-fill"  size="20" @click="playAudioOnce(item.url)"></u-icon>
					<u-icon style="margin-left: 10px;margin-right: 10px"  name="download"  size="20" @click="downloadfile(item.url)"></u-icon>
				</view>
				<view style="width: 90%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.1rem;
				display: flex;flex-direction:row;align-items:center;padding-top:5px;padding-bottom:5px
				;" v-for="(item,index) in soundlist.special" >
					<text style="margin-left: 10px;">{{item.name}}</text>
					<u-icon style="margin-left: auto;margin-right: 10px"  name="play-circle-fill"  size="20" @click="playAudioOnce(item.url)"></u-icon>
					<u-icon style="margin-left: 10px;margin-right: 10px"  name="download"  size="20" @click="downloadfile(item.url)"></u-icon>
				</view>
			<view style="width: 100%;height: 20px;opacity: 0;">1</view>	
			</view>
		</u-transition>
		<!--周表-->
		<u-transition :show="page==0&&show" mode="fade" v-if="sub>=6">
		    <view class="scroll-container"  :style="{width:type==0?'40%':'95%',marginLeft:type==0?'auto':'2.5%',marginRight:type==0?'auto':'2.5%',backgroundColor:color}" style="height: 85vh;border-radius: 10px;margin-top: 20px;overflow-y: auto;display: flex;align-items: center;flex-direction: column;">
				<view style="width: 90%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.5rem;
				display: flex;align-items: center;justify-content: center;padding-top:5px;padding-bottom:5px
				;">
					<text>{{"本周周表"}}</text>
				</view>
				<view style="width: 88%;margin-left: 0%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: auto;border-radius: 5px;font-size: 1.2rem;
				display: flex;flex-direction: row;;padding:1%;justify-content: space-around;margin-top:10px;margin-bottom: 10px
				;" :style="{fontSize:type==0?'20px':'14px'}">
					<view :style="{color:bg==1?fontcolor:'#909399',fontSize:type==0?'1vw':'20px'}" @click="sub3=0,bg=1,change3(1)">天选姬_Official</view>
					<view :style="{color:bg==3?fontcolor:'#909399',fontSize:type==0?'1vw':'20px'}" @click="sub3=1,bg=3,change3(3)">ElevenOfficial_</view>
					<view :style="{color:bg==2?fontcolor:'#909399',fontSize:type==0?'1vw':'20px'}" @click="sub3=2,bg=2,change3(2)">RO姬_Official</view>
				</view>
				<image v-show='bg==1' @click="openpage1('https://space.bilibili.com/703405')" src="https://image.begonia.cafe/tx/date.webp" style="width:95%;margin-left: 2.5%;;margin-top: 2%;margin-bottom: 0%;" mode="widthFix"></image>
				<image v-show='bg==2' @click="openpage1('https://space.bilibili.com/3494357252442916')" src="https://image.begonia.cafe/tx/date1.webp" style="width: 90%;height: 85%;margin-top: 2%;margin-bottom: 0%;" mode="widthFix"></image>
				<image v-show='bg==3' @click="openpage1('https://space.bilibili.com/1639389144')" src="https://image.begonia.cafe/tx/date2.webp" style="width: 90%;height: 85%;margin-top: 2%;margin-bottom: 0%;" mode="heightFix"></image>
				<view style="width: 100%;height: 20px;opacity: 0;">1</view>
			</view>
		</u-transition>
		<!--数据-->
		<u-transition :show="page==1&&show" mode="fade" v-if="sub>=6">
		    <view class="scroll-container" :style="{width:type==0?'40%':'95%',marginLeft:type==0?'auto':'2.5%',marginRight:type==0?'auto':'2.5%',backgroundColor:color}" style="height: 85vh;border-radius: 10px;margin-top: 20px;overflow-y: auto;"
			v-if="live!=null&&live.channel!=null"
			>
				<view style="width: 90%;margin-left: 5%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.5rem;;
				display: flex;align-items: center;justify-content: center;padding-top:5px;padding-bottom:5px
				;">
					<text>{{"直播列表"}}</text>
				</view>
				<view style="width: 88%;margin-left: 5%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: auto;border-radius: 5px;font-size: 1.2rem;
				display: flex;flex-direction: row;;padding:1%;justify-content: space-around;margin-top:10px;margin-bottom: 10px
				;" :style="{fontSize:type==0?'20px':'14px'}">
					<view :style="{color:sub3==0?fontcolor:'#909399',fontSize:type==0?'20px':'20px'}" @click="sub3=0,getlivedata(703405)">天选姬_Official</view>
					<view :style="{color:sub3==1?fontcolor:'#909399',fontSize:type==0?'20px':'20px'}" @click="sub3=1,getlivedata(1639389144)">ElevenOfficial_</view>
					<view :style="{color:sub3==2?fontcolor:'#909399',fontSize:type==0?'20px':'20px'}" @click="sub3=2,getlivedata(3494357252442916)">RO姬_Official</view>
				</view>
				<view style="width: 88%;margin-left: 5%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: auto;border-radius: 5px;font-size: 1.2rem;
				display: flex;flex-direction: row;;padding:1%;margin-top:10px;margin-bottom: 10px;justify-content: center;
				;" :style="{fontSize:type==0?'20px':'14px'}" v-if="sub3==0">
					<text v-if="!live.channel.isLiving">{{"距离璇宝上次开播已经过去了"}}</text>
					<text v-if="!live.channel.isLiving"style="color:rgb(0, 184, 135)">{{time}}</text>
					<text v-if="!live.channel.isLiving">{{"个世纪"}}</text>
					<text v-if="live.channel.isLiving">{{"美丽优雅知性成熟大方的璇宝正在直播"}}</text>
				</view>
				<view style="width: 88%;margin-left: 5%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: auto;border-radius: 5px;font-size: 1.8rem;
				display: flex;flex-direction: row;;padding:1%;justify-content: space-around;margin-top:10px;margin-bottom: 10px
				;" :style="{fontSize:type==0?'1.1rem':'14px'}" @click="linkto()">
					<view style="display: flex;flex-direction: column;" v-if="type==0">
						<text>{{live.channel.uName}}</text>
						<text>{{"房间号:"+live.channel.roomId}}</text>
					</view>
					<view style="display: flex;flex-direction: column;" v-if="type==0">
						<text>{{"直播总场次:"+live.channel.totalLiveCount}}</text>
						<text>{{"直播总时长:"+formatDuration(live.channel.totalLiveSecond)}}</text>
					</view>
					<view style="display: flex;flex-direction: column;" v-if="type==0">
						<text>{{"当前直播状态:"+(live.channel.isLiving==true?'直播中':'未直播')}}</text>
						<text>{{"总弹幕:"+live.channel.totalDanmakuCount}}</text>
					</view>
					<view style="display: flex;flex-direction: column;" v-if="type==1">
						<text>{{live.channel.uName}}</text>
						<text>{{"房间号:"+live.channel.roomId}}</text>
						<text>{{"当前直播状态:"+(live.channel.isLiving==true?'直播中':'未直播')}}</text>
					</view>
					<view style="display: flex;flex-direction: column;" v-if="type==1">
						<text>{{"直播总场次:"+live.channel.totalLiveCount}}</text>
						<text>{{"直播总时长:"+formatDuration(live.channel.totalLiveSecond)}}</text>
						<text>{{"总弹幕:"+live.channel.totalDanmakuCount}}</text>
					</view>
				</view>
				<view style="width: 88%;margin-left: 5%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.8rem;
				display: flex;flex-direction: column;height: auto;padding:1%
				;" @click="linkto()">
					<view style="width: 100%;height: 100%;margin-bottom: 10px;border-bottom: 0.5px solid #efefef;display: flex;flex-direction: row;align-items: center;padding-top: 0px;padding-bottom: 10px " v-for="(item,index) in live.lives"
					v-if="type==0"
					>
						<img referrerpolicy="no-referrer"  :src="item.coverUrl" style="height: 120px;width:auto;border-radius: 5px;margin-right: 10px;" mode="heightFix"></img>
						<view style="height: 120px;width: auto;display: flex;flex-direction: column">
							<text style="font-size: 1.3rem;":style="{color:fontcolor}">{{item.title}}</text>
							<text style="font-size: 1.1rem;">{{getdate(item.startDate)+" "+getxingqi(item.startDate)}}</text>
							<text style="font-size: 1.1rem;">{{gettime(item.startDate)+" - "+gettime(item.stopDate)}}</text>
							<text style="font-size: 1.1rem;">{{"直播时长:"+getDuration(item.startDate,item.stopDate)}}</text>	
						</view>
					</view>
					<view style="width: 100%;height: 100%;margin-bottom: 10px;border-bottom: 0.5px solid #efefef;display: flex;flex-direction: row;align-items: center;padding-top: 0px;padding-bottom: 10px; " v-for="(item,index) in live.lives"
					v-if="type==1"
					>
						<img :src="'https://images.weserv.nl/?url='+item.coverUrl" style="height: 80px;min-width: 150px;max-width:150px;border-radius: 5px;margin-right: 10px;min-width: 100px;" mode="aspectFill" referrerpolicy="no-referrer"></img>
						<view style="height: 100px;width: auto;display: flex;flex-direction: column">
							<text style="font-size: 1rem;":style="{color:fontcolor}">{{item.title}}</text>
							<text style="font-size: 14px;">{{getdate(item.startDate)+" "+getxingqi(item.startDate)}}</text>
							<text style="font-size: 14px;">{{gettime(item.startDate)+" - "+gettime(item.stopDate)}}</text>
							<text style="font-size: 14px;">{{"直播时长:"+getDuration(item.startDate,item.stopDate)}}</text>	
						</view>
					</view>
				</view>
				<view style="width: 100%;height: 20px;opacity: 0;">1</view>
			</view>
			<view class="scroll-container" :style="{width:type==0?'40%':'95%',marginLeft:type==0?'auto':'2.5%',marginRight:type==0?'auto':'2.5%',backgroundColor:color}" style="height: auto;border-radius: 10px;margin-top: 20px;overflow-y: auto;"
			v-else
			>
				<view style="width: 88%;margin-left: 5%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: auto;border-radius: 5px;font-size: 1.8rem;
				display: flex;flex-direction: row;;padding:1%;justify-content: space-around;margin-top:10px;margin-bottom: 10px
				;" :style="{fontSize:type==0?'20px':'14px'}">
				 Danmakus接口错误，请等待服务恢复
				</view>
			</view>
		</u-transition>
		<!--切片-->
		<u-transition :show="page==2&&show" mode="fade" v-if="sub>=6">
		    <view class="scroll-container" :style="{width:type==0?'40%':'95%',marginLeft:type==0?'auto':'2.5%',marginRight:type==0?'auto':'2.5%',backgroundColor:color}" style="height: 85vh;border-radius: 10px;margin-top: 20px;overflow-y: auto;">
				<view style="width: 90%;margin-left: 5%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;
				display: flex;align-items: center;justify-content: center;padding-top:5px;padding-bottom:5px
				;">
					<view style="display: flex;flex-direction: row;align-items: center;width: 80%;justify-content: space-around">
						<view :style="{color:sub1==0?fontcolor:'#909399',fontSize:type==0?'20px':'20px'}" @click="sub1=0,getvideolist(),show3=false">全部</view>
						<view :style="{color:sub1==1?fontcolor:'#909399',fontSize:type==0?'20px':'20px'}" @click="sub1=1,getvideolist(),show3=false">歌切</view>
						<view :style="{color:sub1==2?fontcolor:'#909399',fontSize:type==0?'20px':'20px'}" @click="sub1=2,getvideolist(),show3=false">切片</view>
						<view :style="{color:sub1==3?fontcolor:'#909399',fontSize:type==0?'20px':'20px'}" @click="sub1=3,getvideolist(),show3=false">二创</view>
						<view :style="{color:show3==true?fontcolor:'#909399',fontSize:type==0?'20px':'20px'}" v-if="type==0" @click="show3=true,sub1=-1,sub2=0,anchor_name='天选姬_Official',live_uid=703405,gethistory(703405)">录播</view>
					</view>
					
				</view>
				<view style="width: 90%;margin-left: 5%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 1.8rem;border-radius: 5px;
				display: flex;align-items: center;justify-content: center;padding-top:5px;padding-bottom:5px
				;" v-if="show3">
					<view style="display: flex;flex-direction: row;align-items: center;width: 100%;justify-content: space-around">
						<view :style="{color:sub2==0?fontcolor:'#909399',fontSize:type==0?'1vw':'20px'}" @click="sub2=0,anchor_name='天选姬_Official',live_uid=703405,gethistory(703405)">天选姬_Official</view>
						<view :style="{color:sub2==1?fontcolor:'#909399',fontSize:type==0?'1vw':'20px'}" @click="sub2=1,anchor_name='ElevenOfficial_',live_uid=1639389144,gethistory(1639389144)">ElevenOfficial_</view>
						<view :style="{color:sub2==2?fontcolor:'#909399',fontSize:type==0?'1vw':'20px'}" @click="sub2=2,anchor_name='RO姬_Official',live_uid=3494357252442916,gethistory(3494357252442916)">RO姬_Official</view>
					</view>
					
				</view>
				<view style="width: 88%;margin-left: 5%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.8rem;
				display: flex;flex-direction: column;height: auto;padding:1%;
				;" v-if="history.length>0&&show3">
					<view style="width: 100%;height: 100%;margin-bottom: 10px;border-bottom: 0.5px solid #efefef;display: flex;flex-direction: row;align-items: center;padding-top: 0px;padding-bottom: 10px " v-for="(item,index) in history"
					
					>
						<img referrerpolicy="no-referrer" :src="item.live_info.cover" style="height: 120px;max-width: 200px;;min-width: 200px;border-radius: 5px;margin-right: 15px;" mode="aspectFill"></img>
						<view style="height: 120px;width: 100%;display: flex;flex-direction: column">
							<text style="font-size: 1.1rem;" :style="{color:fontcolor}">{{item.live_info.title}}</text>
							<text style="font-size: 1.1rem;">{{getdate(item.start_time*1000)+" "+getxingqi(item.start_time*1000)}}</text>
							<text style="font-size: 1rem">{{gettime(item.start_time*1000)+"-"+gettime(item.end_time*1000)}}</text>
							<view style="width: 100px;display: flex;align-items: center;justify-content: center;border-radius: 5px;margin-top: 10px;;margin-right: auto;
							color:white;height: 40px;font-size: 1.1rem;
							" @click="openpage1('https://live.bilibili.com/web-cut/quick-publish.html?start_time='+item.start_time+'&end_time='+item.end_time+'&live_key='+item.live_key+'&cover='+item.live_info.cover+'&anchor_id='+live_uid+'&anchor_name='+anchor_name)" 
							:style="{backgroundColor:fontcolor}"
							>
								<text>{{"去剪辑"}}</text>
							</view>
						</view>
					</view>
				</view>
				<view style="width: 88%;margin-left: 5%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.8rem;
				display: flex;flex-direction: column;height: auto;padding:1%;
				;" v-if="videolist.length>0&&show3==false">
					<view style="width: 100%;height: 100%;margin-bottom: 10px;border-bottom: 0.5px solid #efefef;display: flex;flex-direction: row;align-items: center;padding-top: 0px;padding-bottom: 10px " v-for="(item,index) in videolist"
					@click="openpage(item.bv)" v-if="type==0"
					>
						<img :src="item.pic" style="height: 120px;max-width: 200px;;min-width: 200px;border-radius: 5px;margin-right: 15px;" mode="aspectFill" referrerpolicy="no-referrer"></img>
						<view style="height: 120px;width: 100%;display: flex;flex-direction: column">
							<text style="font-size: 1.1rem;":style="{color:fontcolor}">{{item.title}}</text>
							<u--text size="16" lines="2" color="rgb(96, 98, 102)" :text="(item.desc).replaceAll('\n','')"></u--text>
							<view style="display: flex;flex-direction: row;align-items: center;font-size: 1rem;width: 100%;">
								<img referrerpolicy="no-referrer" :src="item.face" style="width: 35px;height: 35px;border-radius: 50%;margin-right: 10px;" mode="aspectFill"></img>
								<text>{{item.author}}</text>
								<view style="font-size: 1rem;margin-left: auto;">{{"类型:"+(item.type==1?'歌切':(item.type==2?'切片':'二创'))}}</view>
							</view>
							
						</view>
					</view>
					<view style="width: 100%;height: 100%;margin-bottom: 10px;border-bottom: 0.5px solid #efefef;display: flex;flex-direction: row;align-items: center;padding-top: 0px;padding-bottom: 10px " v-for="(item,index) in videolist"
					@click="openpage(item.bv)" v-if="type==1"
					>
						<img :src="item.pic" style="height: 120px;min-width: 200px;max-width:200px;border-radius: 5px;margin-right: 10px;" mode="aspectFill" referrerpolicy="no-referrer"></img>
						<view style="height: 120px;width: 100%;display: flex;flex-direction: column">
							<text style="font-size: 14px;":style="{color:fontcolor}">{{item.title}}</text>
							<u--text size="12" lines="2" color="rgb(96, 98, 102)" :text="(item.desc).replaceAll('\n','')"></u--text>
							<view style="display: flex;flex-direction: row;align-items: center;font-size: 12px;width: 100%;">
								<img referrerpolicy="no-referrer" :src="item.face" style="width: 1.4rem;height: 1.4rem;border-radius: 50%;margin-right: 10px;" mode="aspectFill"></img>
								<text>{{item.author}}</text>
								<view style="font-size: 12px;margin-left: auto;">{{"类型:"+(item.type==1?'歌切':(item.type==2?'切片':'二创'))}}</view>
							</view>
							
						</view>
					</view>
				</view>
				<view style="width: 100%;height: 20px;opacity: 0;">1</view>
			</view>
		</u-transition>    
		<!--留言板-->
		<u-transition :show="page==4&&show" mode="fade" v-if="sub>=6">
		    <view class="scroll-container"  :style="{width:type==0?'40%':'95%',marginLeft:type==0?'auto':'2.5%',marginRight:type==0?'auto':'2.5%',backgroundColor:color}" style="height: 85vh;border-radius: 10px;margin-top: 20px;overflow-y: auto;">
				<view style="width: 90%;margin-left: 5%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.5rem;
				display: flex;align-items: center;justify-content: center;padding-top:5px;padding-bottom:5px
				;">
					<text>{{"留言板"}}</text>
				</view>
				<view style="width: 88%;margin-left: 5%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.8rem;
				display: flex;flex-direction: column;height: auto;padding:1%;
				;" v-if="juge(messagelist)">
					<view style="width: 100%;height: 100%;margin-bottom: 10px;border-bottom: 0.5px solid #c6cad1;display:flex;flex-direction:column;padding-top: 0px;padding-bottom: 10px; " v-for="(item,index) in messagelist"
					v-if="item.author=='天选姬'||item.author=='天选姬_Official'"
					>	
						<view style="display: flex;flex-direction: row;align-items: center;">
							<text style="font-size: 1.4rem;color:black" v-if="item.title!=null&&item.title!=''">{{item.title}}</text>
							
						</view>
						<text style="font-size: 1.3rem;color:#484a4d;" :style="{marginTop:(item.title!=null&&item.title!='')?'12px':'0px'}">{{item.data}}</text>
						<view style="display: flex;flex-direction: row;align-items: center;margin-top: 15px;position: relative;height: 80px;">
							<view style="width: 60px;height: 60px;position: relative;margin-right: 10px;">
								<img  referrerpolicy="no-referrer" :src="frame" style="width: 60px;height: 60px;border-radius: 50%;object-fit: cover;position: absolute;z-index: 2;">
								<img  referrerpolicy="no-referrer" src="https://i1.hdslb.com/bfs/face/97c9320b2eef3e92d25025684301c89493b99a1a.jpg" style="width: 50px;height: 50px;border-radius: 50%;object-fit: cover;position: absolute;z-index: 1;top:50%;left:50%;transform:translate(-50%,-50%);">
								
							</view>
							<view style="width: 200px;">
								<view style="font-size: 1.4rem;margin-top: 0px;color:black;font-family:sans-serif">{{item.author}}</view>
								<view style="margin-left: auto;font-size: 1.1rem;margin-top: 0px;margin-right: 5%;">{{getdate1(item.createtime*1000)}}</view>
							</view>
							
							
							<image style="opacity: 0.4;height:100px;position: absolute;bottom:-10px;right:-10px" mode="heightFix"src="../../static/2.webp"></image>
						</view>
						
					</view>
				</view>
				<view style="width: 88%;margin-left: 5%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.8rem;
				display: flex;flex-direction: column;height: auto;padding:1%;
				;">
					<view style="width: 100%;height: 100%;margin-bottom: 10px;border-bottom: 0.5px solid #c6cad1;display:flex;flex-direction:column;padding-top: 0px;padding-bottom: 10px; " v-for="(item,index) in messagelist"
					v-if="item.author!='天选姬'&&item.author!='天选姬_Official'"
					>
						<text style="font-size: 1.2rem;color:#46484b" v-if="item.title!=null&&item.title!=''">{{item.title}}</text>
						<text style="font-size: 1.1rem;" :style="{marginTop:(item.title!=null&&item.title!='')?'12px':'0px'}">{{item.data}}</text>
						<view style="display: flex;flex-direction: row;align-items: center;margin-top: 15px;">
							<view style="font-size: 1.1rem;margin-top: 15px">{{"by "+item.author}}</view>
							<view style="margin-left: auto;font-size: 1.1rem;margin-top: 15px">{{getdate(item.createtime*1000)}}</view>
						</view>
						
					</view>
				</view>
				<view style="width: 100%;height: 20px;opacity: 0;">1</view>
			</view>
		</u-transition>    
		<!--素材-->
		<u-transition :show="page==5&&show" mode="fade" v-if="sub>=6">
		    <view class="scroll-container"  :style="{width:type==0?'40%':'95%',marginLeft:type==0?'auto':'2.5%',marginRight:type==0?'auto':'2.5%',backgroundColor:color,fontSize:type==0?'1.5vh':'1.15rem'}" style="height: 85vh;border-radius: 10px;margin-top: 20px;overflow-y: auto;">
				<view style="width: 90%;margin-left: 5%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 50px;border-radius: 5px;
				display: flex;;padding-top:5px;padding-bottom:5px;flex-direction: column
				;" v-for="(item,index) in aiimagelist">
					<view style="display: flex;flex-direction: row;align-items: center;width: 95%;margin-left: 2.5%">
						<text>{{(index+1)+'. '+item.title}}</text>
						<view style="margin-left: auto;">{{"作者:"+item.author}}</view>
					</view>
					<view style="display: flex;flex-direction: row;align-items: center;width: 95%;margin-left: 2.5%">
						<view style="margin-left: 2.5%;">{{item.url}}</view>
						<view style="margin-left: auto;" :style="{color:fontcolor}" @click="openpage1(item.url)">{{"点击下载"}}</view>
					</view>
				</view>
				<view style="width: 90%;margin-left: 5%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 4vh;border-radius: 5px;font-size: 1.4rem;
				display: flex;;padding-top:5px;padding-bottom:5px;flex-direction: column;align-items: center;justify-content: center
				;">
					表情包合集
				</view>
				<view style="width: 88%;margin-left: 5%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.8rem;
				display: flex;flex-direction: row;height: auto;padding:1%;flex-wrap: wrap;justify-content: space-around
				;">
					<view style="width: 100px;height: 100px;margin:10px" v-for="(item,index) in emojilist" @click="openpage1('http://image.begonia.cafe/tx/emoji/'+item)">
						<image :src="'http://image.begonia.cafe/tx/emoji/'+item" style="width: 100%;height: 100%" mode="aspectFill"></image>
					</view>
					<view style="width: 100px;height: 100px;margin:10px" v-for="i in (5-(emojilist.length%5))">
						
					</view>
				</view>
				<view style="width: 100%;height: 20px;opacity: 0;">1</view>
			</view>
		</u-transition>    
		<!--星姬天故事-->
		<u-transition :show="page==7&&show" mode="fade" v-if="sub>=6">
			<view
			:style="{width:type==0?'40%':'95%',marginLeft:type==0?'auto':'2.5%',marginRight:type==0?'auto':'2.5%',backgroundColor:color,height:type==0?'85%':'85%'}" 
			class="scroll-container"
			style="border-radius: 10px;margin-top: 20px;overflow-y: auto;overflow-x: hidden;display: flex;flex-direction: column;align-items: center;">
				<view style="width: 90%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.4rem;
				display: flex;align-items: center;justify-content: center;padding-top:5px;padding-bottom:5px
				;" >
					<text>{{"星姬天故事"}}</text>
				</view>
				<view style="width: 88%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: auto;border-radius: 5px;font-size: 1.1rem;
				display: flex;flex-direction:column;padding:1%
				;" >
					<view style="width: 100%;display: flex;flex-direction: column;align-items: center;justify-content: center;margin-top: 10px;">
						<image src="/static/星姬天logo.webp" style="height: 13vh;margin-bottom: 20px;" mode="heightFix"></image>
						<image src="/static/title.webp" style="width: 50%;margin-bottom: 20px;" mode="widthFix"></image>
					</view>
					<view v-html="vhtml4"></view>
					
				</view>
				<view style="width: 90%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.4rem;
				display: flex;align-items: center;justify-content: center;padding-top:5px;padding-bottom:5px
				;" >
					<text>{{"永远都陪着璇宝的星姬天们"}}</text>
				</view>
				<view style="width: 90%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: auto;border-radius: 5px;font-size: 1.1rem;
				display: flex;padding-top:5px;padding-bottom:5px;flex-direction: row;flex-wrap: wrap
				;" >
					<view style="width: 100%;">
						<text style="margin:5px;" v-if="item.type==1" v-for="(item,index) in user">{{item.name}}</text>
						
					</view>
					<text style="margin:5px" v-if="item.type==0" v-for="(item,index) in user">{{item.name}}</text>	
					<text style="margin:5px" >{{'明前海棠'}}</text>	
				</view> 
				<view style="width: 90%;margin-top: 10px;background-color: rgba(255,255,255,0.8);max-height:120px;height:auto;border-radius: 5px;font-size: 1.1rem;
				display: flex;;padding-top:5px;padding-bottom:5px;display: flex;flex-direction: row;align-items: flex-start;
				;" >
					<image src="/static/cat.png" style="width: 30px;height: 30px;margin-left: 5px;" mode="aspectFill"></image>
					<text style="margin:5px;margin-left:5px;width: 80px;min-width: 80px">{{"特别感谢:"}}</text>
					<view style="display: flex;flex-direction: row;align-items: center;flex-wrap: wrap;width: 100%;">
						<text style="margin:5px;margin-left:5px;">{{"天选姬家的喵"}}</text>
						<text style="margin:5px;margin-left:5px;">{{"RO姬_Official"}}</text>
						<text style="margin:5px;margin-left:5px;">{{"ElevenOfficial_"}}</text>
						<text style="margin:5px;margin-left:5px;">{{"槙鸟ZENA"}}</text>
						<text style="margin:5px;margin-left:5px;">{{"走路摇ZLY"}}</text>
						<text style="margin:5px;margin-left:5px;">{{"小黄鸡吖_"}}</text>
					</view>
				</view>
				<view style="width: 90%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.4rem;
				display: flex;align-items: center;justify-content: center;padding-top:5px;padding-bottom:5px
				;" >
					<text>{{"星姬天签名墙"}}</text>
				</view>
				<view style="width: 90%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: auto;border-radius: 5px;font-size: 1.1rem;
				display: flex;;padding-top:5px;padding-bottom:5px;
				;" >
					<image @click="pre('https://image.begonia.cafe/tx/sign.png')" mode="widthFix" src="https://image.begonia.cafe/tx/sign.png" style="width: 95%;margin-left:2.5%;margin-top: 10px;margin-bottom: 10px;border-radius: 5px;"></image>
				</view>
				<view style="width: 90%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.4rem;
				display: flex;align-items: center;justify-content: center;padding-top:5px;padding-bottom:5px
				;" >
					<text>{{"璇宝非官方粉丝群:829950771"}}</text>
				</view>	
				<view style="width: 100%;height: 20px;opacity: 0;">1</view>
			</view>
		</u-transition>
		<!--关于-->
		<u-transition :show="page==3&&show" mode="fade" v-if="sub>=6">
			<view  
			:style="{width:type==0?'40%':'95%',marginLeft:type==0?'auto':'2.5%',marginRight:type==0?'auto':'2.5%',backgroundColor:color,}" 
			class="scroll-container"
			style="height: 85vh;border-radius: 10px;margin-top: 20px;overflow-y: auto;overflow-x: hidden;">
		    <view style="width: 90%;margin-left:2.5%;;margin-top: 10px;background-color: rgba(255,255,255,0.8);border-radius: 5px;flex-direction: column;
		    display: flex;align-items: center;justify-content: center;padding-top:5px;padding-bottom:5px;padding-left: 2.5%;padding-right: 2.5%;position: relative
		    ;" >
				<view style="width: 88%;margin-left: 5%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: auto;border-radius: 5px;font-size: 1.8rem;
				display: flex;flex-direction: row;;padding:1%;justify-content: space-around;margin-top:10px;margin-bottom: 10px;
				;" :style="{fontSize:type==0?'20px':'14px'}">
					<view :style="{color:bg==1?fontcolor:'#909399',fontSize:type==0?'1vw':'20px'}" @click="change3(1),sub4=0">天选姬_Official</view>
					<view :style="{color:bg==2?fontcolor:'#909399',fontSize:type==0?'1vw':'20px'}" @click="change3(2),sub4=2">RO姬_Official</view>
					<view :style="{color:bg==3?fontcolor:'#909399',fontSize:type==0?'1vw':'20px'}" @click="change3(3),sub4=1">ElevenOfficial_</view>
				</view>
		    	<view v-html="vhtml1" :class="{'op2':bg==1,'op1':bg!=1}" style="transition: 0.5s;position: absolute;top:100px;background-color: rgba(255,255,255,0.8);border-radius:5px;
				;width: 95%;padding:2.5%;
				" :style="{zIndex:bg==1?'3':'-2'}" v-if="bg==1"></view>
				<view v-html="vhtml2" :class="{'op2':bg==2,'op1':bg!=2}" style="transition: 0.5s;position: absolute;top:100px;background-color: rgba(255,255,255,0.8);border-radius:5px
				;width: 95%;padding:2.5%;"  v-if="bg==2" :style="{zIndex:bg==2?'2':'-2'}"></view>
				<view v-html="vhtml3" :class="{'op2':bg==3,'op1':bg!=3}" style="transition: 0.5s;position: absolute;top:100px;background-color: rgba(255,255,255,0.8);border-radius:5px
				;width: 95%;padding:2.5%;" :style="{zIndex:bg==3?'1':'-2'}" v-if="bg==3"></view>
				</view>
				
				
				
			</view>
		</u-transition> 
		<!--文章-->
		<u-transition :show="page==8&&show" mode="fade" v-if="sub>=6">
			<view  
			:style="{width:type==0?'40%':'95%',marginLeft:type==0?'auto':'2.5%',marginRight:type==0?'auto':'2.5%',backgroundColor:color,}" 
			class="scroll-container"
			style="height: 85vh;border-radius: 10px;margin-top: 20px;overflow-y: auto;overflow-x: hidden;">
			<view style="width: 90%;margin-left: 5%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.5rem;;
			display: flex;align-items: center;justify-content: center;padding-top:5px;padding-bottom:5px
			;">
				<text>{{"星姬天文选"}}</text>
			</view>
		    <view style="width: 85%;margin-left:5%;margin-top: 10px;background-color: rgba(255,255,255,0.8);border-radius: 5px;flex-direction: column;
		    display: flex;align-items: center;justify-content: center;padding-top:5px;padding-bottom:5px;padding-left: 2.5%;padding-right: 2.5%;position: relative
		    ;" >
					<view style="width: 100%;height: 100%;margin-bottom: 10px;border-bottom: 0.5px solid #efefef;display: flex;flex-direction: row;align-items: center;padding-top: 0px;padding-bottom: 10px " v-for="(item,index) in themelist"
					@click="sub5=index,page=9" v-if="type==0"
					>
						<image :src="item.cover" style="height: 120px;max-width: 200px;;min-width: 200px;border-radius: 5px;margin-right: 15px;" mode="aspectFill"></image>
						<view style="height: 120px;width: 100%;display: flex;flex-direction: column">
							<text style="font-size: 1.1rem;":style="{color:fontcolor}">{{item.title}}</text>
							<u--text size="16" lines="2" color="rgb(96, 98, 102)" :text="getcontent(item.content)"></u--text>
							<view style="display: flex;flex-direction: row;align-items: center;font-size: 1rem;width: 100%;">
								<text>{{"作者:"+item.author}}</text>
							</view>

						</view>
					</view>
					<view style="width: 100%;height: 100%;margin-bottom: 10px;border-bottom: 0.5px solid #efefef;display: flex;flex-direction: row;align-items: center;padding-top: 0px;padding-bottom: 10px " v-for="(item,index) in themelist"
					@click="sub5=index,page=9" v-if="type==1"
					>
						<image :src="item.cover" style="height: 120px;min-width: 200px;max-width:200px;border-radius: 5px;margin-right: 10px;" mode="aspectFill"></image>
						<view style="height: 120px;width: 100%;display: flex;flex-direction: column">
							<text style="font-size: 14px;":style="{color:fontcolor}">{{item.title}}</text>
							<u--text size="12" lines="2" color="rgb(96, 98, 102)" :text="getcontent(item.content)"></u--text>
							<view style="display: flex;flex-direction: row;align-items: center;font-size: 12px;width: 100%;">
								<text>{{"作者:"+item.author}}</text>
							</view>
							
						</view>

					</view>
			</view>
			<view style="width: 100%;height: 20px;opacity: 0;">1</view>
			</view>
		</u-transition> 
		<!--文章详情-->
		<u-transition :show="page==9&&show" mode="fade" v-if="sub>=6&&themelist.length>0">
			<view  
			:style="{width:type==0?'40%':'95%',marginLeft:type==0?'auto':'2.5%',marginRight:type==0?'auto':'2.5%',backgroundColor:color,}" 
			class="scroll-container"
			style="height: 85vh;border-radius: 10px;margin-top: 20px;overflow-y: auto;overflow-x: hidden;">
			<view style="width: 90%;margin-left: 5%;margin-top: 10px;background-color: rgba(255,255,255,0.8);height: 40px;border-radius: 5px;font-size: 1.5rem;;
			display: flex;align-items: center;justify-content: center;padding-top:5px;padding-bottom:5px;position: relative
			;">
				<view style="width: 90%;margin-left: 0%;display: flex;align-items: center;justify-content: center;position: absolute;">{{themelist[sub5].title}}</view>
				<u-icon name="arrow-left" style="position: absolute;top:0;bottom:0;left:2%;z-index: 111;" size="20" @click="page=8"></u-icon>
			</view>
			<view style="width: 85%;margin-left:5%;margin-top: 10px;background-color: rgba(255,255,255,0.8);border-radius: 5px;flex-direction: column;
			display: flex;;padding-top:5px;padding-bottom:5px;padding-left: 2.5%;padding-right: 2.5%;position: relative
			;" >
				<view v-html="themelist[sub5].content.replaceAll('cut-off','<br>')"></view>
				<view style="margin-top: 20px;width: 100%;">{{"作者:"+themelist[sub5].author}}</view>
				<view style="margin-top: 20px;width: 100%;color:#3c9cff" v-if='themelist[sub5].url&&themelist[sub5].url!="None"&&themelist[sub5].url!="null"' @click="openpage1(themelist[sub5].url)">{{"B站专栏:"+themelist[sub5].url}}</view>
			
			</view>
			<view style="height: 20px;width: 100%;opacity: 0;">
				1
			</view>
			</view>
		</u-transition> 
		<!---->
		<u-transition :show="page==4&&show" mode="fade" v-if="sub>=6">
		    <view style="position: fixed;right:20px;bottom:20px;height: 65px;width: 65px;border-radius: 50%;display: flex;align-items: center;justify-content: center; "
			@click="show1=true" :style="{backgroundColor:color}"
			>
				<u-icon name="plus" color="white" size="55"></u-icon>
			</view>
		</u-transition> 
		<u-transition :show="page==2&&show" mode="fade" v-if="sub>=6&&type==0">
		    <view style="position: fixed;right:20px;bottom:20px;height: 65px;width: 65px;border-radius: 50%;display: flex;align-items: center;justify-content: center; "
			@click="show2=true"  :style="{backgroundColor:color}"
			>
				<u-icon name="plus" color="white" size="55"></u-icon>
			</view>
		</u-transition> 
		<u-transition :show="page==8&&show" mode="fade" >
		    <view style="position: fixed;right:20px;bottom:20px;height: 65px;width: 65px;border-radius: 50%;display: flex;align-items: center;justify-content: center; "
			@click="show5=true"  :style="{backgroundColor:color}"
			>
				<u-icon name="plus" color="white" size="55"></u-icon>
			</view>
		</u-transition> 
		<!--开屏动画-->
		
		<view style="position: fixed;width: 100%;height: 100%;position: fixed;z-index: 9999;display: flex;align-items: center;justify-content: center;background-color: white;top:0;flex-direction: column;transition: 0.5s;"
		:class="{'op2':sub<=4,'op1':sub>=5}" v-if="sub!=6"
		>
			<view style="display: flex;flex-direction: row;align-items: center;justify-content: center;font-size: 50px;color:#00ffbf;transition: 0.5s;position: fixed;top:auto;bottom:auto;left:auto;right:auto"
			:class="{'op2':sub==0,'op1':sub!=0}"
			>
				<text>{{'Loading'}}</text>
				<text v-for="x in i">{{'.'}}</text>
			</view>
			<image src="/static/星姬天logo.webp" @load="waiting" style="width: 20vh;max-width: 250px;max-height:250px;;height: 20vh;;transition: 0.5s;" mode="aspectFit"
			:class="{'op1':sub<3,'op2':sub>=3,'op3':sub>=3&&type==0,'op4':sub>=3&&type==1}"
			></image>
			<image src="/static/doro2.webp" @load="waiting" style="width:20vw;height: 20vw;;transition: 0.5s;position: fixed;top:auto;" mode="aspectFit"
			:style="{left:sub>=3?(type==1?'4vw':'10vw'):'-55vw',bottom:type==0?'auto':'45vh'}"
			></image>
			<image src="/static/doro1.webp" @load="waiting" style="width:20vw;height: 20vw;;transition: 0.5s;position: fixed;top:auto;" mode="aspectFit"
			:style="{right:sub>=3?(type==1?'4vw':'10vw'):'-55vw',bottom:type==0?'auto':'45vh'}"
			></image>
			<image  @load="waiting" src="/static/title.webp" style="transition: 0.5s;height: 20vh;max-height:20vh;position: absolute;top:auto;bottom:auto;left:auto;right:auto" :style="{width:type==0?'50vw':'95vw'}" :mode="type==0?'heightFix':'widthFix'" :class="{'op1':sub<=3,'op2':sub==4}" ></image>
		</view>
		<!---->
		<u-popup :show="show1" @close="show1=false"  mode="center" bgColor="transparent">
		    <view style="height: 70vh;background-color: rgba(255,255,255,0.75);border-radius: 10px;padding:1%" :style="{width:type==0?'38vw':'90vw'}">
		       <text style="font-size: 1.3rem;">标题</text>
			   <view style="background-color: rgba(255,255,255,0.9);border-radius: 5px;margin-top: 10px;">
					<u--input
					placeholder="请输入留言的标题"
					border="surround"
					fontSize="18"
					v-model="title"
					></u--input>   
			   </view>
			   <text style="font-size: 1.3rem;">署名</text>
			   <view style="background-color: rgba(255,255,255,0.9);border-radius: 5px;margin-top: 10px;">
			   		<u--input
			   		placeholder="请输入留言署名"
			   		border="surround"
			   		fontSize="18"
			   		v-model="author"
			   		></u--input>   
			   </view>
			    <text style="font-size: 1.3rem;">正文</text>
				<view style="background-color: rgba(255,255,255,0.9);border-radius: 5px;margin-top: 10px;">
					<u--textarea
					placeholder="请输入留言内容"
					border="surround"
					fontSize="18"
					v-model="data"
					height="400"
					count
					maxlength="500"
					></u--textarea>   
				</view>
				<view style="width: 200px;display: flex;align-items: center;justify-content: center;border-radius: 5px;margin-top: 10px;margin-left: auto;margin-right: auto;
				;color:white;height: 40px;font-size: 1.1rem;
				" @click="newmessage()" :style="{backgroundColor:fontcolor}">
					<text>{{"提交"}}</text>
				</view>
		    </view>
		</u-popup>
		<!---->
		<u-popup :show="show2" @close="show2=false"  mode="center" bgColor="transparent">
		    <view style="height: 70vh;width: 38vw;background-color: rgba(255,255,255,0.75);border-radius: 10px;padding:1%">
		       <text style="font-size: 1.3rem;">BV</text>
			   <view style="display: flex;flex-direction: row;align-items: center;width: 100%;">
					<view style="background-color: rgba(255,255,255,0.9);border-radius: 5px;margin-top: 10px;width: 85%;">
										<u--input
										placeholder="请输入视频的BV号"
										border="surround"
										fontSize="18"
										v-model="bv"
										></u--input>   
					</view>
					<view style="width: 13%;margin-left: 2%;height: 40px;display: flex;align-items: center;justify-content: center;border-radius: 5px;margin-right: 10px;color:white;margin-top: 10px;"
					@click="getvideoinfo()" :style="{backgroundColor:fontcolor}"
					>					
						解析视频
					</view>
			   </view>	  
			   <text style="font-size: 1.3rem;margin-top: 10px;">视频类型</text>
			   <view style="display: flex;flex-direction: row;align-items:center;border-radius: 5px;margin-top: 10px;">
			   		<view style="width: 80px;height: 35px;display: flex;align-items: center;justify-content: center;border-radius: 5px;margin-right: 10px;"
					:style="{backgroundColor:videotype==0?fontcolor:'white',color:videotype==0?'white':'#909399'}" @click="videotype=0"
					>
						歌切
					</view>
					<view style="width: 80px;height: 35px;display: flex;align-items: center;justify-content: center;border-radius: 5px;margin-right: 10px;"
					:style="{backgroundColor:videotype==1?fontcolor:'white',color:videotype==1?'white':'#909399'}" @click="videotype=1"
					>
						切片
					</view>
					<view style="width: 80px;height: 35px;display: flex;align-items: center;justify-content: center;border-radius: 5px;"
					:style="{backgroundColor:videotype==2?fontcolor:'white',color:videotype==2?'white':'#909399'}" @click="videotype=2"
					>
						二创
					</view>
			   </view>
			   <text style="font-size: 1.3rem;margin-top: 10px;">视频信息</text>
			   <view style="display: flex;flex-direction: row;align-items: center;margin-top: 10px;" v-if="videoinfo!=null">
				   <img referrerpolicy="no-referrer" :src="videoinfo.pic" style="width: 270px;height: 150px;border-radius: 5px;" mode="cover"></img>
				   <view style="margin-left: 10px;display: flex;flex-direction: column;">
					   <text>{{"标题:"+videoinfo.title}}</text>
					   <view style="display: flex;flex-direction: row;align-items: center;">
							<text>{{"作者:"+videoinfo.owner.name}}</text>
							<img :src="videoinfo.owner.face" style="width: 40px;height: 40px;border-radius: 50%;margin-left: 10px;" mode="aspectFill" referrerpolicy="no-referrer"></img>
					   </view>
						<text>{{'发布日期:'+getdate(videoinfo.ctime*1000)+" "+gettime(videoinfo.ctime*1000)}}</text>
				   </view>
			   </view>
			    <view style="display: flex;flex-direction: column;margin-top: 10px;" v-if="videoinfo!=null">
					<text>{{"视频简介"}}</text>
					<text> {{videoinfo.desc}}</text>
				</view>
			   <view style="width: 200px;display: flex;align-items: center;justify-content: center;border-radius: 5px;margin-top: 20px;margin-left: auto;margin-right: auto;
			   ;color:white;height: 40px;font-size: 1.1rem;
			   " @click="newvideo()" v-if="videoinfo!=null" :style="{backgroundColor:fontcolor}">
			   	<text>{{"提交"}}</text>
			   </view>
		    </view>
		</u-popup>
		<!---->
		<u-popup :show="show5" @close="show5=false"  mode="center" bgColor="transparent">
		    <view style="height: 80vh;background-color: rgba(255,255,255,0.75);border-radius: 10px;padding:1%;overflow-y: auto;" :style="{width:type==0?'38vw':'90vw'}">
			   <text style="font-size: 1.3rem;">封面</text>
			    <view style="display: flex;flex-direction: row;align-items: center;width: 100%;margin-top: 10px;">
					  <u-upload
					    :fileList="fileList1"
					    @afterRead="afterRead"
					    @delete="deletePic"
					    name="1"
					    multiple
					    :maxCount="10"
					  ></u-upload>
				</view>
		       <text style="font-size: 1.3rem;">标题</text>
			   <view style="display: flex;flex-direction: row;align-items: center;width: 100%;">
					<view style="background-color: rgba(255,255,255,0.9);border-radius: 5px;margin-top: 10px;width: 85%;">
							<u--input
										placeholder="请输入文章标题"
										border="surround"
										fontSize="18"
										v-model="theme.title"
							></u--input>   
					</view>
				</view>
				<text style="font-size: 1.3rem;">作者</text>
				<view style="display: flex;flex-direction: row;align-items: center;width: 100%;">
					<view style="background-color: rgba(255,255,255,0.9);border-radius: 5px;margin-top: 10px;width: 85%;">
							<u--input
										placeholder="请输入署名"
										border="surround"
										fontSize="18"
										v-model="theme.author"
							></u--input>   
					</view>
				</view>  
				<text style="font-size: 1.3rem;">B站专栏/动态地址</text>
				<view style="display: flex;flex-direction: row;align-items: center;width: 100%;">
					<view style="background-color: rgba(255,255,255,0.9);border-radius: 5px;margin-top: 10px;width: 85%;">
							<u--input
										placeholder="可留空"
										border="surround"
										fontSize="18"
										v-model="theme.url"
							></u--input>   
					</view>
				</view>  
				<text style="font-size: 1.3rem;">正文</text>
				<view style="background-color: rgba(255,255,255,0.9);border-radius: 5px;margin-top: 10px;">
					<u--textarea
					placeholder="请输入文章内容"
					border="surround"
					fontSize="18"
					v-model="theme.content"
					height="300"
					count
					maxlength="5000"
					></u--textarea>   
				</view>
			   <view style="width: 200px;display: flex;align-items: center;justify-content: center;border-radius: 5px;margin-top: 20px;margin-left: auto;margin-right: auto;
			   ;color:white;height: 40px;font-size: 1.1rem;
			   " @click="newtheme" :style="{backgroundColor:fontcolor}">
			   	<text>{{"提交"}}</text>
			   </view>
		    </view>
		</u-popup>
		<test style='height: 100vh;width: 100vw;position: fixed;z-index: 999999;top:0;left:0;' v-if="show9" @close="closed1"></test>
		<u-popup :show="showinfo" @close="showinfo=false"  mode="center" bgColor="transparent" zIndex='999'>
			<view style="height: auto;width: auto;padding:1vh;background-color: rgba(255,255,255,0.8);display: flex;align-items:center;flex-direction: column;border-radius: 10px;z-index: 1;"
			@click="openpage1('https://live.bilibili.com/2058234')" v-if="type==0"
			>
				<text style="font-size: 4vh;font-style:italic;font-weight: 700;color:aqua;text-shadow: #909399 2px 1.5px 3px;margin-top: 3vh;margin-bottom: 3vh;">{{'本周日程表'}}</text>
				<image style="width: 50vw;height: auto;" mode="widthFix" src="https://image.begonia.cafe/tx/date.webp">
					
				</image>
				<!-- <view style="width: 30vw;height: 30vw;box-shadow: 0px 0px 15px #909399;border-radius: 5px;overflow: hidden;display: flex;flex-direction: row;
				flex-wrap: wrap;
				;">
					<image src="https://image.begonia.cafe/tx/info/1.webp" style="width: 10vw;height: 10vw;" mode="aspectFill" ></image>
					<image src="https://image.begonia.cafe/tx/info/2.webp" style="width: 10vw;height: 10vw;" mode="aspectFill" ></image>
					<image src="https://image.begonia.cafe/tx/info/3.webp" style="width: 10vw;height: 10vw;" mode="aspectFill" ></image>
					<image src="https://image.begonia.cafe/tx/info/4.webp" style="width: 10vw;height: 10vw;" mode="aspectFill" ></image>
					<image src="https://image.begonia.cafe/tx/info/5.webp" style="width: 10vw;height: 10vw;" mode="aspectFill" ></image>
					<image src="https://image.begonia.cafe/tx/info/6.webp" style="width: 10vw;height: 10vw;" mode="aspectFill" ></image>
					<image src="https://image.begonia.cafe/tx/info/7.webp" style="width: 10vw;height: 10vw;" mode="aspectFill" @click.stop="pre('https://image.begonia.cafe/tx/info/10.webp')"></image>
					<image src="https://image.begonia.cafe/tx/info/8.webp" style="width: 10vw;height: 10vw;" mode="aspectFill" @click.stop="pre('https://image.begonia.cafe/tx/info/11.webp')"></image>
					<image src="https://image.begonia.cafe/tx/info/9.webp" style="width: 10vw;height: 10vw;" mode="aspectFill" @click.stop="pre('https://image.begonia.cafe/tx/info/12.webp')"></image>
				</view> -->
			</view>
			<view style="height: auto;width: auto;padding:1vh;background-color: rgba(255,255,255,0.8);display: flex;align-items:center;flex-direction: column;border-radius: 10px;z-index: 1;"
			@click="openpage1('bilibili://live/2058234')" v-else
			>
				<text style="font-size: 3vh;font-style:italic;font-weight: 700;color:aqua;text-shadow: #909399 2px 1.5px 3px;margin-top: 1vh;margin-bottom: 1vh;">{{'本周日程表'}}</text>
				<image style="width: 90vw;height: auto;" mode="widthFix" src="https://image.begonia.cafe/tx/date.webp">
					
				</image>
				<!-- <view style="width: 90vw;height: 90vw;box-shadow: 0px 0px 15px #909399;border-radius: 5px;overflow: hidden;display: flex;flex-direction: row;
				flex-wrap: wrap;
				;">
					<image src="https://image.begonia.cafe/tx/info/1.webp" style="width: 30vw;height: 30vw;" mode="aspectFill" ></image>
					<image src="https://image.begonia.cafe/tx/info/2.webp" style="width: 30vw;height: 30vw;" mode="aspectFill" ></image>
					<image src="https://image.begonia.cafe/tx/info/3.webp" style="width: 30vw;height: 30vw;" mode="aspectFill" ></image>
					<image src="https://image.begonia.cafe/tx/info/4.webp" style="width: 30vw;height: 30vw;" mode="aspectFill" ></image>
					<image src="https://image.begonia.cafe/tx/info/5.webp" style="width: 30vw;height: 30vw;" mode="aspectFill" ></image>
					<image src="https://image.begonia.cafe/tx/info/6.webp" style="width: 30vw;height: 30vw;" mode="aspectFill" ></image>
					<image src="https://image.begonia.cafe/tx/info/7.webp" style="width: 30vw;height: 30vw;" mode="aspectFill" @click.stop="pre('https://image.begonia.cafe/tx/info/10.webp')"></image>
					<image src="https://image.begonia.cafe/tx/info/8.webp" style="width: 30vw;height: 30vw;" mode="aspectFill" @click.stop="pre('https://image.begonia.cafe/tx/info/11.webp')"></image>
					<image src="https://image.begonia.cafe/tx/info/9.webp" style="width: 30vw;height: 30vw;" mode="aspectFill" @click.stop="pre('https://image.begonia.cafe/tx/info/12.webp')"></image>
				</view> -->
			</view>
		</u-popup>
	</view>
</template>
<script>
	import test from '../test/test.vue'
	import progres from "../progress/progress.vue"
	export default {
		components:{
			test,progres
		},
		computed: {
		    '-webkit-scrollbar-thumb'() {
				return {
						'--color':'rgba(207,0,0,0.4)',
						'--fontcolor':"rgba(85, 0, 127, 1.0)",
					}
				}
		},
		data() {
			return {
				isplay:false,
				progress:0,
				musiclist:[
					{
						name:"我只选你",
						url:'https://image.begonia.cafe/tx/music/我只选你.mp3',
						cover:'https://image.begonia.cafe/tx/music/我只选你.jpg',
						//text:"https://image.begonia.cafe/tx/music/我只选你.lrc"
						text:"/static/我只选你.lrc"
					},
					{
						name:"天选的你",
						url:'https://image.begonia.cafe/tx/music/天选的你.mp3',
						cover:'https://image.begonia.cafe/tx/music/天选的你.jpg',
						//text:"https://image.begonia.cafe/tx/music/天选的你.lrc"
						text:"/static/天选的你.lrc"
					},
					{
						name:"超时空守候",
						url:'https://image.begonia.cafe/tx/music/超时空守候.mp3',
						cover:'https://image.begonia.cafe/tx/music/超时空守候.jpg',
						//text:"https://image.begonia.cafe/tx/music/超时空守候.lrc"
						text:"/static/超时空守候.lrc"
					},
					{
						name:"梦想的光芒",
						url:'https://image.begonia.cafe/tx/music/梦想的光芒.mp3',
						cover:'https://image.begonia.cafe/tx/music/梦想的光芒.webp',
						//text:"https://image.begonia.cafe/tx/music/梦想的光芒.lrc"
						text:"/static/梦想的光芒.lrc"
					},
				],
				textlist:[
					
				],
				musicindex:0,
				time:0,
				title1:"快乐星姬天制作委员会",
				user:[],
				direction: 'right',
				      style: '',
				      width: 500,
				      height: 500,
				      size: 350,
				modelPath: {
				    type: String,
				    default: '@/static/l2d/a.json'
				},
				canvasWidth: {
				    type: Number,
				    default: 300
				},
				canvasHeight: {
				    type: Number,
				    default: 400
				},
				theme:{
					title:"",
					author:"",
					content:"",
					url:null
				},
				bg4:true,
				fileList1:[],
				first:true,
				show:false,
				show1:false,
				show2:false,
				show3:false,
				show4:false,
				show5:false,
				show6:false,
				show7:false,
				show8:false,
				show9:true,
				show10:false,
				show11:false,
				showinfo:false,
				scrollTop:0,
				lyricLineHeight:21.67,
				sub:2,
				sub1:0,
				sub2:0,
				sub3:0,
				sub4:0,
				sub5:0,
				page:3,
				musictext:"等待播放",
				num:0,
				timer:null,
				timer1:null,
				timer2:null,
				i:0,
				live:{},
				live_id:"",
				noise:true,
				live_uid:"",
				anchor_name:"",
				livesub:-1,
				bg:'',
				type:0,
				data:"",
				musicshow:false,
				musicautoshow:false,
				musicautoplay:false,
				color:"rgba(38, 255, 208, 0.45)",
				//color:"rgba(207, 0, 0, 0.4)",
				//color:"rgba(122, 75, 0, 0.4)",
				fontcolor:"#00b887",
				//fontcolor:"rgba(207, 0, 0, 0.6)",
				//fontcolor:"rgba(122, 75, 0, 0.7)",
				author:"",
				messagelist:[],
				baseurl:"",
				videoinfo:null,
				videotype:0,
				videolist:[],
				title:"",
				margin:0,
				bv:"",
				frame:"",
				bg:1,
				scale:1,
				scale1:1,
				vhtml1:"",
				vhtml2:"",
				vhtml3:"",
				vhtml4:"",
				aiimagelist:[],
				emojilist:[],
				history:[],
				bvlist:[],
				videoHidden:false,
				setting1:true,
				setting2:false,
				vw1:1,
				themelist:[],
				music:null,
				currentLyricIndex:0,
				soundlist:{
					normal:[
						{
							url:"https://image.begonia.cafe/tx/sound/1.mp3",
							name:"日常语音1"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/2.mp3",
							name:"日常语音2"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/3.mp3",
							name:"日常语音3"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/4.mp3",
							name:"日常语音4"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/5.mp3",
							name:"日常语音5"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/6.mp3",
							name:"日常语音6"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/7.mp3",
							name:"日常语音7"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/8.mp3",
							name:"日常语音8"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/9.mp3",
							name:"日常语音9"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/10.mp3",
							name:"日常语音10"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/11.mp3",
							name:"日常语音11"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/12.mp3",
							name:"日常语音12"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/13.mp3",
							name:"日常语音13"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/14.mp3",
							name:"日常语音14"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/15.mp3",
							name:"日常语音15"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/16.mp3",
							name:"日常语音16"
						},
					],
					special:[
						{
							url:"https://image.begonia.cafe/tx/sound/天选元旦.mp3",
							name:"元旦语音",
							date:"01-01"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/天选春节.mp3",
							name:"春节语音",
							date:"01-28"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/天选开学31.mp3",
							name:"春季开学语音",
							date:"03-01"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/天选出道.mp3",
							name:"出道日语音",
							date:"03-17"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/天选劳动.mp3",
							name:"劳动节语音",
							date:"05-01"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/天选六一.mp3",
							name:"儿童节语音",
							date:"06-01"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/天选端午.mp3",
							name:"端午节语音",
							date:"06-19"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/天选开学91.mp3",
							name:"秋季开学语音",
							date:"09-01"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/天选中秋.mp3",
							name:"中秋节语音",
							date:"10-06"
						},	
						{
							url:"https://image.begonia.cafe/tx/sound/天选国庆.mp3",
							name:"国庆节语音",
							date:"10-01"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/天选万圣.mp3",
							name:"万圣节语音",
							date:"11-01"
						},
						{
							url:"https://image.begonia.cafe/tx/sound/天选圣诞.mp3",
							name:"圣诞节语音",
							date:"12-25"
						},
						
					],
					audioUrl:null,
					audio:null,
					app:null,
				},
				showdorosub:3,
				timer3:null,
				showdorosub1:true,
				vh1:1,
				lyricList:[],
			}
		},
		onReady() {
			
			const systemInfo = uni.getSystemInfoSync();
			const isPortrait = systemInfo.screenHeight > systemInfo.screenWidth;
			if (isPortrait) {
				this.type=1;
				this.bg4=true;
				uni.setStorageSync("index",'old')
			} else {
			
				if(uni.getStorageSync("index")=='new'){
					uni.reLaunch({
						url:"/pages/index/index"
					})
					return;
				}else{
					uni.setStorageSync("index",'old')
				}
				this.type=0;
				this.vw1=systemInfo.screenWidth
				
				const container = document.querySelector('.scroll-container');
				const infoDisplay = document.getElementById('height-info');
				// 计算80%高度（像素值）
				const viewportHeight = window.innerHeight;
				const width = window.innerWidth
				this.margin=width
				const windowResizeCallback = (res) => {
					 const width = window.innerWidth
					 this.margin=width
					 
					 this.$forceUpdate();
				}
				uni.onWindowResize(windowResizeCallback)
				var sub = 0.88;
				if(viewportHeight<800)sub=0.8
				var targetHeight =0;
				try {
				   targetHeight = viewportHeight * sub;
				   container.style.height = `${targetHeight}px`;
				  // 应用高度
				}
				catch(err) {
				   
				}
				
				// 显示当前高度信息（调试用）
				//infoDisplay.textContent = `当前视口高度: ${viewportHeight}px | 容器高度: ${targetHeight}px (80%)`;
				const designWidth = 2048;
				
				// 计算基准字体大小
				const baseFontSize = (this.vw1 / designWidth) * 12 * window.devicePixelRatio;
				document.documentElement.style.fontSize = `${baseFontSize}px`;
			}
			let that=this;
			   
		},
		onUnload(){
			this.music=null;
		},
		onLoad() {
			this.loadsetting();
			if(uni.getStorageSync("showdoro")==false||uni.getStorageSync("showdoro")==null){
				uni.setStorageSync("showdoro",3);
				this.show8=true;
			}else{
				this.showdorosub=uni.getStorageSync("showdoro");
				this.show8=true;
			}
			var bg4=uni.getStorageSync("bg4");
			if(bg4=='a1'||bg4==null||bg4==false){
				this.bg4=true;
			}
			else if(bg4=='a2'){
				this.bg4=false;
			}
			let that=this;
			var x=0
			this.timer=setInterval(()=>{
				if(this.isplay){
					
				}
			},10)
			this.timer2=setInterval(()=>{
				if(that.showdorosub1==true){
				var sub = Math.floor(Math.random() * 2000);
				if((sub<=that.showdorosub*20)&&that.showdorosub1){
					that.showdorosub1=false;
					that.showdoro();
					x=0;
				}else{
					x++;
					if(x==20){
						x=0;
						if(that.showdorosub!=0){
							that.showdorosub1=false;
							that.showdoro();
						}
					}
				}
				}
			},3000)
			this.fetchLrc();
			this.timer=setInterval(()=>{
				if(that.title1=='这里是美丽优雅成熟知性大方的璇宝 快来和天选姬贴贴~'){
					that.title1='快乐星姬天制作委员会';
				}
				else{
					that.title1='这里是美丽优雅成熟知性大方的璇宝 快来和天选姬贴贴~'
				}
				uni.setNavigationBarTitle({ title:that.title1 });
			},30000)
			this.timer1=setInterval(()=>{
				if(that.live!=null&&that.live.lives!=null&&that.live.lives[0].stopDate!=null){
					var end = that.live.lives[0].stopDate
					var now = new Date().getTime();
					that.time=parseInt((now-end)/1000);
				}
			},1000)
			setTimeout(()=>{
				//that.load()
			},500)
			this.updateScrollbarStyle(this.color);
			setInterval(()=>{
				if(that.i+1==4){
					that.i=0
				}else that.i++
			},500)
			this.baseurl="/api/"
			uni.request({
				url:this.baseurl+"getuserlist",
				method:"POST",
				data:{
					
				},
				success: (res) => {
					this.user=res.data.data;
				}
			})
			uni.request({
				url:this.baseurl+"getinfo",
				method:"POST",
				data:{
					
				},
				success: (res) => {
					
					this.vhtml1=res.data.data[0].info;
					this.vhtml2=res.data.data[1].info;
					this.vhtml3=res.data.data[2].info;
				}
			})
			uni.request({
				url:this.baseurl+"getframe",
				method:"POST",
				data:{
					
				},
				success: (res) => {
					res = res.data
					if(res.new_pendants!=null&&res.new_pendants.frame!=null&&res.new_pendants.frame.value!=null&&res.new_pendants.frame.value!=''){
						this.frame=res.new_pendants.frame.value
					}else{
						this.frame='https://i0.hdslb.com/bfs/live/30cc1c9eb6e8b5bd6a8894fd3c2ef019ccce76d1.png'
						//this.frame="/static/frame.png"
					}
				}
			})
			uni.request({
				url:this.baseurl+"getaiimagelist",
				method:"POST",
				data:{
					
				},
				success: (res) => {
					this.aiimagelist=res.data.data;
				}
			})
			uni.request({
				url:this.baseurl+"getemojilist",
				method:"POST",
				data:{
					
				},
				success: (res) => {
					this.emojilist=res.data.data;
				}
			})
			uni.request({
				url:this.baseurl+"getintroduce",
				method:"POST",
				data:{
					
				},
				success: (res) => {
					this.vhtml4=res.data.data[0].content;
				}
			})
			uni.request({
				url:this.baseurl+"getbvlist",
				method:"POST",
				data:{
					
				},
				success: (res) => {
					this.bvlist=res.data.data;
				}
			})
			this.getlivedata(703405);
			this.getmessage();
			this.getvideolist();
			uni.getImageInfo({
				src:"https://image.begonia.cafe/tx/bg.webp",
				success: (res) => {
					this.waiting()
				}
			})
			this.getthemelist()
			
		},
		methods: {
			linkto1(e){
				if(e=='/pages/new/new'){
					uni.setStorageSync("index",'new');
				}
				uni.navigateTo({
					url:e
				})
			},
			async progresschange(e){
				if(this.isplay==true){
					const duration = this.music.duration;
					this.music.currentTime = parseInt(duration / 100 * e)
					this.progress=e;
				}else{
					await this.musicplay();
					let that=this;
					setTimeout(()=>{
						const duration = that.music.duration;
						that.music.currentTime = parseInt(duration / 100 * e)
						that.progress=e;
					},100)
					
				}
			},
			last(){
	
				if(this.isplay==true){
					
					this.musicstop();
					if(this.musicindex==0){
						this.musicindex=this.musiclist.length-1
					}else{
						this.musicindex=this.musicindex-1;
					}
					this.fetchLrc();
					this.music=null;
					this.musicplay();
				}else{
					if(this.musicindex==0){
						this.musicindex=this.musiclist.length-1
					}else{
						this.musicindex=this.musicindex-1;
					}
					this.fetchLrc();
					this.music=null;
				}
				this.scrollTop=Math.random();
				this.$forceUpdate();
			},
			next(){
				if(this.isplay==true){
					this.musicstop();
					if(this.musicindex+1==this.musiclist.length){
						this.musicindex=0
					}else{
						this.musicindex=this.musicindex+1;
					}
					this.fetchLrc();
					this.music=null;
					this.musicplay();
				
				}else{
					if(this.musicindex+1==this.musiclist.length){
						this.musicindex=0
					}else{
						this.musicindex=this.musicindex+1;
					}
					this.fetchLrc();
					this.music=null;
				}
				this.scrollTop=Math.random();
				this.$forceUpdate();
			},
			 async fetchLrc() {
			      try {
			        const res = await uni.request({
			          url: this.musiclist[this.musicindex].text,
			          method: 'GET'
			        });
			        
			        if (res.statusCode === 200) {
			          const lrcText = res.data;
			          this.lyricList = this.parseLrc(lrcText);
			        } else {
			          console.error('LRC文件请求失败', res.statusCode);
			        }
			      } catch (err) {
			        console.error('LRC请求错误', err);
			      }
			    },
			    
			    /**
			     * 解析LRC歌词文本
			     * LRC格式示例：[00:01.23]歌词内容
			     */
			    parseLrc(lrcText) {
			      const lines = lrcText.split('\n'); // 按行分割
			      const lyricList = [];
			      
			      // 正则匹配时间轴 [mm:ss.ms]
			      const timeReg = /\[(\d{2}):(\d{2})\.(\d{2,3})\]/;
			      
			      lines.forEach(line => {
			        if (!line) return; // 跳过空行
			        
			        const timeMatch = line.match(timeReg);
			        if (timeMatch) {
			          // 提取分、秒、毫秒
			          const minute = parseInt(timeMatch[1]);
			          const second = parseInt(timeMatch[2]);
			          const millisecond = parseInt(timeMatch[3]);
			          
			          // 转换为总秒数（保留2位小数）
			          const totalSeconds = minute * 60 + second + millisecond / 100;
			          
			          // 提取歌词文本（去除时间轴部分）
			          const text = line.replace(timeReg, '').trim();
			          
			          if (text) {
			            lyricList.push({
			              time: totalSeconds,
			              text: text
			            });
			          }
			        }
			      });
			      
			      // 按时间排序（防止LRC文件中时间顺序混乱）
			      return lyricList.sort((a, b) => a.time - b.time);
			    },
			syncLyric(currentTime) {
			      // 遍历歌词数组，找到当前时间对应的歌词
			      for (let i = 0; i < this.lyricList.length; i++) {
			        // 当前歌词的时间 <= 当前播放时间，且下一句歌词的时间 > 当前播放时间
			        const isCurrent = this.lyricList[i].time <= currentTime;
			        const isNext = i + 1 < this.lyricList.length 
			          ? this.lyricList[i + 1].time > currentTime 
			          : true;
			        
			        if (isCurrent && isNext) {
			          // 更新当前歌词索引
					  
			          if (this.currentLyricIndex !== i) {
			            this.currentLyricIndex = i;
			            // 滚动到当前歌词（居中显示）
						const systemInfo = uni.getSystemInfoSync();
						var height = systemInfo.windowHeight;
						
			            this.scrollTop = (i - 1) * height*0.02;
			          }
			          break;
			        }
				}
			},
			async musicplay(){
				if(this.music==null){
					this.music = new Audio(this.musiclist[this.musicindex].url);
					await this.fetchLrc(this.musiclist[this.musicindex].text);
					if(this.noise){
						this.music.volume=0.5
					}else{
						this.music.volume=0
					}
					let that=this;
					this.music.addEventListener('timeupdate', function() {
					  // currentTime 属性表示当前播放位置（秒）
					  
					  const currentTime = that.music.currentTime;
					  that.syncLyric(currentTime)
					  // duration 属性表示音频总时长（秒）
					  const duration = that.music.duration;
					  
					  // 计算进度百分比
					  const progress = (currentTime / duration) * 100;
					  that.progress = progress;
					  // 处理时间更新逻辑（例如更新进度条）
					 
					  // updateProgressBar(progress); // 更新进度条的自定义函数
					});
					this.music.addEventListener('ended', function() {
					  that.isplay=false;
					});
				}
				let that=this;
				this.music.play()
				    .then(() => {
				        that.isplay=true;
					
				    })
				    .catch(error => {
				        console.error('播放失败:', error);
				});
			},
			musicstop(){
				this.isplay=false;
				if(this.music!=null){
					this.music.pause();
				}
			},
			opennoise(){
				this.noise=true;
				this.music.volume=0.5
			},
			stopnoise(){
				this.noise=false
				this.music.volume=0
			},
			closed1(){
				let that=this;
				setTimeout(()=>{
					that.show9=false;
					that.load()
				},500)
			},
			changeshowdoro(e){
				uni.setStorageSync("showdoro",e);
			},
			showdoro(){
				let that=this;
				that.show6=true;
				var sub = Math.floor(Math.random() * 100)
				if(sub<=33&&sub>0){
					that.show7=true;
					setTimeout(()=>{
						that.show6=false;
						setTimeout(()=>{
							that.show7=false;
							that.showdorosub1=true;
						},10)
					},6000)
				}else if(sub<=66&&sub>33){
					that.show10=true;
					setTimeout(()=>{
						that.show6=false;
						setTimeout(()=>{
							that.show10=false;
							that.showdorosub1=true;
						},10)
						
					},3000)
				}else{
					that.show11=true;
					setTimeout(()=>{
						that.show6=false;
						setTimeout(()=>{
							that.show11=false;
							that.showdorosub1=true;
						},10)
						
					},4500)
				}
			},
			pre(e){
				uni.previewImage({
					urls:[e],
				})
			},
			juge(e){
				for(var x=0;x<e.length;x++){
					if(e[x].author=='天选姬'||e[x].author=='天选姬_Official')
						return true;
				}
			},
			linkto(){
				if(this.sub3==0){
					window.open("https://live.bilibili.com/2058234")
				}
				if(this.sub3==2){
					window.open("https://live.bilibili.com/30326232")
				}
				if(this.sub3==1){
					window.open("https://live.bilibili.com/25896305")
				}
			},
			getcontent(e){
				e = e.replaceAll('<br>',' ')
				e = e.replaceAll('cut-off'," ")
					return e
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
					    .trim();
			},
			newtheme(){
				if(this.theme.title==''){
					uni.showToast({
						icon:"none",
						title:"请输入标题"
					})
					return;
				}
				if(this.theme.content==''){
					uni.showToast({
						icon:"none",
						title:"请输入正文内容"
					})
					return;
				}
				if(this.theme.author==''){
					uni.showToast({
						icon:"none",
						title:"请输入正文署名"
					})
					return;
				}
				if(this.fileList1.length==0){
					uni.showToast({
						icon:"none",
						title:"请上传文章封面"
					})
					return;
				}
				this.theme.cover="https://image.begonia.cafe/tx/emoji/"+this.fileList1[0].name;
				this.theme.content = this.theme.content.replace(/\n/g, "<br>");
				uni.request({
					url:'api/newtheme',
					method:"POST",
					data:this.theme,
					success: (res) => {
						if(res.data.code==1001){
							this.show5=false;
							uni.showToast({
								icon:"none",
								title:"上传成功，请等待审核"
							})
							this.theme={
								title:"",
								content:"",
								author:"",
								url:null,
							}
						}else{
							uni.showToast({
								icon:"none",
								title:res.data.msg
							})
						}
					}
				})
				
			},
			getthemelist(){
				uni.request({
					url:this.baseurl+"getthemelist",
					method:"POST",
					data:{},
					success: (res) => {
						this.themelist=res.data.data
					}
				})
			},
			getScale(w = 2048 , h = 1026 ) {
				const systemInfo = uni.getSystemInfoSync();
			    const ww = systemInfo.screenWidth / w;//算出scale需要的比例 * w = 当前宽度
			    const wh = systemInfo.screenHeight / h;
				
			    //缩小最大是1920,缩小的比例参数效果是保持有一个适应边宽或边长的。
			    return ww
			},
			 updateScrollbarStyle(color) {
			      // 先移除旧的动态样式（避免重复）
			      const oldStyle = document.getElementById('dynamic-scrollbar-style');
			      if (oldStyle) {
			        oldStyle.remove();
			      }
			
			      // 创建新的样式标签
			      const style = document.createElement('style');
				  
			      style.id = 'dynamic-scrollbar-style';
			      // 全局样式（不使用scoped，确保作用于滚动条伪元素）
			      style.innerHTML = `
			        /* 滚动条轨道 */
			        .scroll-container::-webkit-scrollbar-track {
			          background:${this.color};
			        }
			        /* 滚动条滑块 */
			        .scroll-container::-webkit-scrollbar-thumb {
			          background: ${this.fontcolor};
			          border-radius: 6px;
			        }
			        /* 滚动条滑块hover状态 */
			        .scroll-container::-webkit-scrollbar-thumb:hover {
			          background: ${this.fontcolor}; /* 稍微变亮 */
			        }
			        /* 滚动条宽度 */
			        .scroll-container::-webkit-scrollbar {
			          width: 6px;
			        }
			      `;
			
			      // 插入到页面头部
			      document.head.appendChild(style);
			    },
			downloadfile(e){
				window.open(e)
			},
			change1(e){
				uni.setStorageSync("setting1",this.setting1)
			},
			change2(e){
				uni.setStorageSync("setting2",this.setting2)
			},
			change5(e){
				uni.setStorageSync("musicshow",e);
			},
			change3(e){
				
				if(e==1||e==2||e==3){
					this.bg=e;
				}else{
					if(this.bg+1>=4)this.bg=1;else this.bg++;
				}
				if(this.bg==1){
					this.color="rgba(38, 255, 208, 0.45)"
					this.fontcolor="#00b887"
				}
				if(this.bg==2){
					this.color="rgba(207, 0, 0, 0.4)"
					this.fontcolor="rgba(207, 0, 0, 0.6)"
				}
				if(this.bg==3){
					this.color="rgba(122, 75, 0, 0.4)"
					this.fontcolor="rgba(122, 75, 0, 0.7)"
				}
				this.updateScrollbarStyle();
				this.$forceUpdate();
				uni.setStorageSync("bg",this.bg);
			},
			change4(){
				this.bg4=!this.bg4;
				if(this.bg4==true)
				uni.setStorageSync("bg4",'a1');
				else uni.setStorageSync("bg4",'a2')
			},
			loadsetting(){
				var setting1 = uni.getStorageSync("setting1");
				var setting2 = uni.getStorageSync("setting2");
				var bg=uni.getStorageSync("bg");
				if((bg!=1&&bg!=2&&bg!=3)){
					bg=1
					uni.setStorageSync("bg",1)
				}
				this.bg=bg;
				this.change3(this.bg);
				this.$forceUpdate()
				var juge = uni.getStorageSync("first");
				if(juge==false||(uni.getStorageSync("musicshow")==''&&uni.getStorageSync("musicshow")!=false)){
					uni.setStorageSync("musicshow",true)
				}

				this.musicautoshow=uni.getStorageSync("musicshow");
				if(uni.getStorageSync("setting1")==null||uni.getStorageSync("setting1")==''||uni.getStorageSync("setting1")==undefined){
					
					if(setting1==false&&juge==false){
						setting1=true;
						uni.setStorageSync("setting1",setting1)

					}
				}
				if(uni.getStorageSync("setting2")==null||uni.getStorageSync("setting2")==''||uni.getStorageSync("setting2")==undefined){
					if(setting2==false&&juge==false){
						setting2=false;
						uni.setStorageSync("setting2",setting2)
					}
				}
				if(juge==false){
					uni.setStorageSync("first",true)
				}
				this.setting1=setting1
				this.setting2=setting2
				if(this.setting1==false){
					this.show9=false
					this.sub=6;
					this.show=true;
					this.page=3;
					this.musicshow=uni.getStorageSync("musicshow")
					this.showinfo=true;
				}
			},
			jugeaudio(){
				if(this.setting2==false)return;
				var date = new Date();
				var month = date.getMonth()+1;
				if(month<10)month = "0"+month
				var day = date.getDate();
				if(day<10)day = "0"+day
				var date1 = day+"-"+date;
				var url=""
				for(var x=0;x<this.soundlist.special.length;x++){
					var data=this.soundlist.special;
					if(data[x].date==( month+"-"+day)){
						url = data[x].url
						break;
					}
				}
				if(url==''){
					var sub = Math.floor(Math.random() * 16);
					url = this.soundlist.normal[sub].url
				}
				this.playAudioOnce(url)
			},
			playAudioOnce(audioUrl) {
			    // 创建音频对象
				if(this.audio!=null){
					this.audio.pause();
					this.audio.removeAttribute(this.audioUrl);
					this.audio.load();
					this.audio = null;
				}
				this.audioUrl=audioUrl;
			    this.audio = new Audio(this.audioUrl);
			    
			    // 确保音频只播放一次（默认行为，但显式设置更清晰）
			    this.audio.loop = false;
			    
			    // 播放音频
			    this.audio.play()
			        .then(() => {
			            
			        })
			        .catch(error => {
			            console.error('播放失败:', error);
			            // 处理可能的错误，如浏览器自动播放政策限制
			          
			        });
				
			},
			async init() {
				if(this.type==1)return;
				
			},
			onVideoEnded(){
				this.videoHidden=false;
			},
			gethistory(e){
				uni.request({
					url:this.baseurl+"gethistory",
					method:"POST",
					data:{
						live_uid:e,
					},
					success: (res) => {
						this.history=res.data.data.replay_info
						this.$forceUpdate()
					}
				})
			},
			openpage1(e){
				
				window.open(e);
			},
			openpage(e){
				window.open("https://www.bilibili.com/video/"+e)
			},
			getvideolist(){
				let url = this.baseurl+"getvideo"
				
				uni.request({
					url:(url),
					method:"POST",
					data:{
						type:this.sub1
					},
					success: (res) => {
						this.videolist=res.data.data;
						this.$forceUpdate()
					}
				})
			},
			getvideoinfo(){
				var bv = JSON.parse(JSON.stringify(this.bv));
				if(bv.indexOf("https")!=-1){
					bv = bv.split("/")[4]
					this.bv=bv;
				}
				uni.request({
					url:(this.baseurl+"getbilibilivideo"),
					method:"POST",
					data:{
						bv:bv
					},
					success: (res) => {
						this.videoinfo=res.data.data;
					}
				})
			},
			newvideo(){
				if(this.videoinfo==null){
					return;
				}
				for(var x=0;x<this.bvlist.length;x++){
					
					if(this.bv==this.bvlist[x].bv){
						this.message("这个视频已正在审核或已经添加过了")
						return;
					}
				}
				uni.request({
					url:(this.baseurl+"newvideo"),
					method:"POST",
					data:{
						title:this.videoinfo.title,
						pic:this.videoinfo.pic,
						desc:this.videoinfo.desc,
						author:this.videoinfo.owner.name,
						face:this.videoinfo.owner.face,
						bv:this.bv,
						createtime:this.videoinfo.ctime,
						type:this.videotype+1
					},
					success:(res)=>{
						if(res.data.code==1001){
							this.message("提交成功，请等待审核")
							let that=this;
							setTimeout(()=>{
								this.show2=false;
								this.bv="";
								this.videoinfo=null;
							})
						}else{
							this.message("系统错误")
						}
					},
					fail(res){
						this.message("系统错误")
					}
				})
			},
			getmessage(){
				uni.request({
					url:(this.baseurl+"getmessage"),
					method:"POST",
					data:{},
					success: (res) => {
					
						this.messagelist=res.data.data
					}
				})
			},
			message(e){
				uni.showToast({
					icon:"none",
					title:e
				})
			},
			newmessage(){
				if(this.data==''){
					this.message("请输入留言内容");
					return;
				}
				if(this.author==''){
					this.message("请留下署名");
					return;
				}
				uni.request({
					url:(this.baseurl+"newmessage"),
					method:"POST",
					data:{
						title:this.title,
						data:this.data,
						author:this.author
					},
					success: (res) => {
						if(res.data.code==1001){
							this.message(res.data.msg)
							let that=this;
							setTimeout(()=>{
								that.data="";
								that.author="";
								that.show1=false;
								that.getmessage();
							},1500)
							
						}else{
							this.message("系统错误")
						}
					},
					fail: (res) => {
						this.message(res)
					}
				})
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
			getdate1(e){
				const date = new Date(e);
				const year = date.getFullYear();
				const month = String(date.getMonth() + 1).padStart(2, '0'); // 月份从0开始
				const day = String(date.getDate()).padStart(2, '0');
				const hour = String(date.getHours()).padStart(2, '0')
				const min = String(date.getMinutes()).padStart(2, '0')
				const sec = String(date.getSeconds()).padStart(2, '0')
				//return `${year}-${month}-${day} ${hour}:${min}:${sec}`;
				return `${year}-${month}-${day}`;
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
			getlivedata(e){
				uni.request({
					url:this.baseurl+"getbilibiliroom?uid="+e,
					method:"GET",
					success: (res) => {
						this.livesub=1;
						this.live=res.data.data;
						this.$forceUpdate()
					},
					fail: () => {
						this.livesub=0
						
					}
				})
				return;
				uni.request({
					url:this.baseurl+"getbilibiliroom",
					method:"GET",
					success: (res) => {
						this.livesub=1;
					
					},
					fail: () => {
						this.livesub=0
						
					}
				})
			},
			waiting(){
			},
			load(){
				let that=this;
				this.sub=2;
				if(this.setting1==false){
					that.sub=6;
					that.show=true;
					that.musicshow=true;
					that.videoHidden=true
					that.page=3;
					that.showinfo=true;
					return;
				}
				

							that.jugeaudio()
							that.sub=3;
							setTimeout(()=>{
								that.sub=4;
								setTimeout(()=>{
									that.sub=5;
									setTimeout(()=>{
										that.sub=6;
										that.videoHidden=true
										setTimeout(()=>{
											that.show=true;
											
											that.musicshow=uni.getStorageSync("musicshow")
											that.page=3;
											that.showinfo=true;
										},100)
									},800)
								},1000)
							},300)
			},
			deletePic(event) {
			        this[`fileList${event.name}`].splice(event.index, 1);
			      },
			      // 新增图片
			      async afterRead(event) {
			        // 当设置 multiple 为 true 时, file 为数组格式，否则为对象格式
			        let lists = [].concat(event.file);
			        let fileListLen = this[`fileList${event.name}`].length;
			        lists.map((item) => {
			          this[`fileList${event.name}`].push({
			            ...item,
			            status: "uploading",
			            message: "上传中",
			          });
			        });
			        for (let i = 0; i < lists.length; i++) {
			          const result = await this.uploadFilePromise(lists[i].url);
			          let item = this[`fileList${event.name}`][fileListLen];
			          this[`fileList${event.name}`].splice(
			            fileListLen,
			            1,
			            Object.assign(item, {
			              status: "success",
			              message: "",
			              url: result,
			            })
			          );
			          fileListLen++;
			      }
				},
			      uploadFilePromise(url) {
			        return new Promise((resolve, reject) => {
			          let a = uni.uploadFile({
			            url: this.baseurl+"admin/uploadimage", 
			            filePath: url,
			            name: "file",
			            formData: {
			        
			            },
			            success: (res) => {
			              setTimeout(() => {
			                resolve(res.data.data);
			              }, 1000);
			            },
			          });
			        });
			      },
		}
	}
</script>

<style lang="scss" scoped>
.op1{
	opacity: 0;
}
.op2{
	opacity: 1;
}
.op3{
	opacity: 1;
	margin-top: -45vh;
}
.op4{
	opacity: 1;
	margin-top: -25vh;
}
.top1{
	margin-top: -5vh
}
.top2{
	margin-top: 0px;
}
.xuanzhuan1{
	transform: rotate(0deg);
}
.xuanzhuan2{
	transform: rotate(180deg);
}


::-webkit-scrollbar {
		width: 8px !important;
		background: rgba(255,255,255,0) !important;
		display: block !important;
		border-radius: 0 10px 10px 0;
	}

	::-webkit-scrollbar-thumb {
		background-color:rgba(255,255,255,0);
		border-radius: 3px;
	}
.scroll-container{
	transition:0.5s;
	height: 85vh;
	position: fixed;
	left:0;
	right:0;
	margin:0 auto;
	top:8vh
}
//设置滚动条背景颜色
	.cu-dialog::-webkit-scrollbar-track {
		background: #f1f1f1;
	}
html {
font-size: 100%; /* 1rem = 根元素字体大小的100% */
}
.right{
	right:-120px;
}
.left{
	right:100vw;
	transition: 5s linear;
}
.left1{
	right:100vw;
	transition: 2s linear;
}
.left2{
	right:100vw;
	transition: 3.5s linear;
}
.music-player {
  padding: 20rpx;
}

.lyric-container {
  height: 20px;
  border-radius: 16rpx;
}

.lyric-scroll {
  padding: 10rpx;
  text-align: center;
}

.lyric-line {
    height: 2vh; /* 每条歌词高度 */
      line-height: 2vh; /* 文字垂直居中 */
      text-align: center;
      transition: all 0.3s ease;
}

.lyric-line.active {
  color: #3B82F6; /* 高亮当前歌词 */
  font-size: 32rpx;
  font-weight: bold;
}
.unactive1{
	color:#909399;

}
.unactive2{
	color:#909399
}
.rotate-animation {
  animation: rotate 15s linear infinite;
}
@keyframes rotate {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
.progress-container {
  width: 100%;
  padding: 0 20rpx;
  box-sizing: border-box;
}

/* 进度条样式 */
.progress-bar {
  position: relative;
  width: 100%;
  height: 8rpx;
  background-color: #e5e5e5;
  border-radius: 4rpx;
  margin: 20rpx 0;
}

/* 已播放进度 */
.progress-played {
  position: absolute;
  height: 100%;
  background-color: #3B82F6;
  border-radius: 4rpx;
  transition: width 0.1s ease;
}

/* 滑块样式 */
.progress-thumb {
  position: absolute;
  top: 50%;
  width: 24rpx;
  height: 24rpx;
  background-color: #3B82F6;
  border-radius: 50%;
  transform: translate(-50%, -50%);
  box-shadow: 0 0 8rpx rgba(59, 130, 246, 0.6);
  transition: left 0.1s ease;
}

/* 时间显示 */
.time-display {
  display: flex;
  justify-content: space-between;
  font-size: 24rpx;
  color: #666;
}
</style>
