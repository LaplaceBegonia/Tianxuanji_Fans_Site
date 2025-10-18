<template>
  <view class="progress-container">
    <!-- 进度条容器 -->
    <view 
      class="progress-bar" 
      @click="handleProgressClick"
      @touchstart="handleTouchStart"
      @touchmove="handleTouchMove"
      @touchend="handleTouchEnd"
    >
      <!-- 已播放进度 -->
      <view 
        class="progress-played" 
        :style="{ width: progress + '%' }"
      ></view>
      
      <!-- 进度条滑块 -->
      <view 
        class="progress-thumb" 
        :style="{ left: progress + '%' }"
      ></view>
    </view>

  </view>
</template>

<script>
export default {
  props: {
    // 当前进度百分比（0-100）
    progress: {
      type: Number,
      default: 0
    },
    // 音频总时长（秒），用于时间格式化显示
    totalTime: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      // 是否正在拖动
      isDragging: false,
      // 进度条宽度（px）
      barWidth: 0,
      // 当前播放时间（秒）
      currentTime: 0
    };
  },
  watch: {
    // 根据进度百分比计算当前播放时间
    progress(val) {
      if (!this.isDragging) {
        this.currentTime = (val / 100) * this.totalTime;
      }
    }
  },
  methods: {
    /**
     * 点击进度条跳转
     */
    handleProgressClick(e) {
      this.calculateProgress(e);
    },
    
    /**
     * 开始拖动
     */
    handleTouchStart() {
      this.isDragging = true;
      // 获取进度条宽度（px）
      const query = uni.createSelectorQuery().in(this);
      query.select('.progress-bar').boundingClientRect(data => {
        this.barWidth = data.width;
      }).exec();
    },
    
    /**
     * 拖动中（实时更新滑块位置）
     */
    handleTouchMove(e) {
      if (this.isDragging) {
        this.calculateProgress(e);
      }
    },
    
    /**
     * 结束拖动
     */
    handleTouchEnd() {
      this.isDragging = false;
    },
    
    /**
     * 计算点击/拖动位置对应的进度百分比
     */
    calculateProgress(e) {
      // 获取进度条的起始位置

      const query = uni.createSelectorQuery().in(this);
      query.select('.progress-bar').boundingClientRect(data => {
        const barLeft = data.left; // 进度条左边缘坐标
        const barWidth = data.width; // 进度条宽度
        
        // 获取点击/触摸位置的X坐标
        // const clientX = e.type.includes('touch') 
        //   ? e.touches[0].clientX 
        //   : e.clientX;
		const clientX = e.touches[0].clientX 

        // 计算百分比（限制在0-100之间）
        let percent = ((clientX - barLeft) / barWidth) * 100;
        percent = Math.max(0, Math.min(100, percent));
        // 触发进度变更事件（传递给父组件处理）
        this.onProgressChange(percent);
      }).exec();
    },
    
    /**
     * 进度变更处理函数
     * 可在父组件中通过@progress-change监听
     */
    onProgressChange(percent) {
      // 向上传递进度百分比（保留1位小数）
      this.$emit('progress-change', Math.round(percent * 10) / 10);
    },
    
    /**
     * 格式化时间为 MM:SS 格式
     */
    formatTime(seconds) {
      if (isNaN(seconds)) return '00:00';
      const mins = Math.floor(seconds / 60);
      const secs = Math.floor(seconds % 60);
      return `${mins.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
    }
  }
};
</script>

<style scoped>
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
  background-color: #f4f4f4;
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
