<template>
  <div class="app">
    <h1>vue3-border-progress 示例展示</h1>

    <div class="example-container">
      <!-- 示例 1：动态进度 -->
      <div class="example">
        <h3>动态进度</h3>
        <h4>持续变化的进度</h4>
        <div class="app-container">
          <BorderProgress :progress="dynamicProgress">
            <div class="content-demo">
              <div style="font-size: 24px; font-weight: bold;">{{ dynamicProgress }}%</div>
              <div style="font-size: 12px; color: #666;">动态进度</div>
            </div>
          </BorderProgress>
        </div>
        <div class="controls">
          <button @click="startProgress">开始动画</button>
          <button @click="stopProgress">停止动画</button>
        </div>
        <div class="info">自动递增的进度值</div>
      </div>

      <!-- 示例 2：基础用法 -->
      <div class="example">
        <h3>基础用法</h3>
        <h4>默认参数，随机更新进度</h4>
        <div class="app-container">
          <BorderProgress :progress="progress1">
            <div class="content-demo">
              <div style="font-size: 24px; font-weight: bold;">{{ progress1 }}%</div>
              <div style="font-size: 12px; color: #666;">基础用法</div>
            </div>
          </BorderProgress>
        </div>
        <div class="controls">
          <button @click="updateProgress1">随机进度</button>
        </div>
        <div class="info">progress: 0-100, strokeWidth: 4px, 默认颜色</div>
      </div>

      <!-- 示例 3：不同进度值 -->
      <div class="example">
        <h3>不同进度值</h3>
        <h4>展示不同百分比效果</h4>
        <div class="app-container" style="min-height: 180px; padding: 10px 0;">
          <div style="display: flex; flex-direction: column; gap: 15px; align-items: center; width: 100%;">
            <!-- 第一行：0% 25% -->
            <div style="display: flex; justify-content: center; width: 100%;">
              <div v-for="value in [0, 30,60,90]" :key="value" style="display: flex; justify-content: center; align-items: center; margin: 5px;">
                <BorderProgress :progress="value" >
                  <div class="content-demo" style="width:40px;height:40px;">
                    <div style="font-size: 14px; font-weight: bold;">{{ value }}%</div>
                  </div>
                </BorderProgress>
              </div>
            </div>
          </div>
        </div>
        <div class="info">不同 progress 值的视觉效果</div>
      </div>


      <!-- 示例 5：自定义颜色 -->
      <div class="example">
        <h3>自定义颜色</h3>
        <h4>不同主题色展示</h4>
        <div class="app-container">
          <div style="display: flex; gap: 20px; flex-wrap: wrap; justify-content: center;">
            <div class="grid-item" v-for="(color, index) in colors" :key="index">
              <BorderProgress 
                :progress="70" 
                :progress-color="color.progressColor" 
                :background-color="color.backgroundColor"
              >
                <div class="content-demo" :style="{ color: color.progressColor }">
                  <div style="font-size: 16px;">{{ color.text }}</div>
                </div>
              </BorderProgress>
              <div style="margin-top: 10px; font-size: 12px;">{{ color.text === '灰色' ? '紫色主题' : `${color.text}主题` }}</div>
            </div>
          </div>
        </div>
        <div class="info">progressColor/backgroundColor 自定义颜色</div>
      </div>

      <!-- 示例 6：边框宽度 -->
      <div class="example">
        <h3>边框宽度</h3>
        <h4>不同 strokeWidth 效果</h4>
        <div class="app-container" style="min-height: 120px; padding: 10px 0;">
          <div style="display: flex; flex-direction: column; gap: 15px; align-items: center; width: 100%;">
            <!-- 第一行：2px 4px 8px -->
            <div style="display: flex; justify-content: center; width: 100%;">
              <div v-for="width in [2, 4, 8]" :key="width" style="display: flex; justify-content: center; align-items: center; margin: 5px;">
                <BorderProgress :progress="50" :stroke-width="width">
                  <div class="content-demo" style="width: 60px; height: 60px;">
                    <div style="font-size: 14px;">{{ width }}px</div>
                  </div>
                </BorderProgress>
              </div>
            </div>
          </div>
        </div>
        <div class="info">strokeWidth 参数控制边框粗细</div>
      </div>

      <!-- 示例 7：动画速度 -->
      <div class="example">
        <h3>动画速度</h3>
        <h4>不同动画持续时间</h4>
        <div class="app-container">
          <div style="display: flex; gap: 20px; flex-wrap: wrap; justify-content: center;">
            <div class="grid-item" v-for="(item, index) in durationItems" :key="index">
              <BorderProgress 
                :progress="item.progress.value" 
                :animation-duration="item.duration"
              >
                <div class="content-demo" style="width:60px;height:60px;">
                  <div style="font-size: 16px;">{{ item.duration }}ms</div>
                </div>
              </BorderProgress>
              <div class="controls" style="margin-top: 10px;">
                <button @click="updateDurationProgress(index)">{{ index === 0 ? '快速' : index === 1 ? '中速' : '慢速' }}</button>
              </div>
              <div style="margin-top: 5px; font-size: 12px;">{{ item.duration }}ms{{ index === 1 ? ' (默认)' : '' }}</div>
            </div>
          </div>
        </div>
        <div class="info">animationDuration 控制动画速度</div>
      </div>

      <!-- 示例 8：不同内容类型 -->
      <div class="example">
        <h3>不同内容类型</h3>
        <h4>支持各种内容</h4>
        <div class="app-container">
          <div style="display: flex; gap: 30px; justify-content: center;">
            <div v-for="(content, index) in contentTypes" :key="index" style="display: flex; flex-direction: column; align-items: center; margin: 10px;">
              <BorderProgress :progress="65">
                <div class="content-demo" style="width: 80px; height: 80px;">
                  <svg v-if="content.type === 'image'" t="1767669328292" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="1738" width="70" height="70"><path d="M857.6 0H165.888C74.24 0 0 74.24 0 166.4v691.2c0 92.16 74.24 166.4 165.888 166.4h692.224c91.648 0 165.888-74.24 165.888-166.4v-691.2c-0.512-92.16-74.752-166.4-166.4-166.4zM384 686.08c-38.4 0-69.632-7.68-108.544-15.872l-108.544 54.272 31.232-93.184c-77.824-54.272-123.904-123.904-123.904-209.92 0-147.968 139.776-264.192 310.784-264.192 152.576 0 286.208 93.184 312.832 218.112-10.24-1.024-19.456-1.536-30.208-1.536-147.456 0-264.192 110.08-264.192 245.76 0 22.528 3.584 44.544 9.728 65.024-9.728 1.024-19.456 1.536-29.184 1.536z m457.728 108.544l23.04 77.824-84.992-46.592c-31.232 7.68-62.464 15.872-93.184 15.872-147.968 0-264.192-100.864-264.192-225.28 0-123.904 116.224-225.28 264.192-225.28 139.776 0 263.68 101.376 263.68 225.28 0.512 69.632-46.08 131.584-108.544 178.176z" p-id="1739"></path><path d="M237.568 323.072c0 12.288 5.12 24.064 13.312 32.768 8.704 8.704 20.48 13.312 32.768 13.312 12.288 0 24.064-5.12 32.768-13.312 8.704-8.704 13.312-20.992 13.312-32.768 0-12.288-5.12-24.064-13.312-32.768-8.704-8.704-20.992-13.312-32.768-13.312-12.288 0-24.064 5.12-32.768 13.312-8.704 8.704-13.312 20.992-13.312 32.768zM462.336 323.072c0 12.288 5.12 24.064 13.312 32.768s20.992 13.312 32.768 13.312c12.288 0 24.064-5.12 32.768-13.312 8.704-8.704 13.312-20.992 13.312-32.768 0-12.288-5.12-24.064-13.312-32.768-8.704-8.704-20.992-13.312-32.768-13.312-12.288 0-24.064 5.12-32.768 13.312-8.192 8.704-13.312 20.992-13.312 32.768zM574.464 547.328c0 9.216 3.584 18.432 10.752 25.088 6.656 6.144 15.872 10.24 25.088 10.24s18.432-3.584 25.088-10.24c6.656-6.144 10.752-15.872 10.752-25.088s-3.584-18.432-10.752-25.088c-6.656-6.144-15.872-10.24-25.088-10.24s-18.432 3.584-25.088 10.24c-6.656 6.656-10.752 15.872-10.752 25.088zM737.28 547.328c0 9.216 3.584 18.432 10.752 25.088 6.656 6.144 15.872 10.24 25.088 10.24s18.432-3.584 25.088-10.24c6.656-6.144 10.752-15.872 10.752-25.088s-3.584-18.432-10.752-25.088c-6.656-6.144-15.872-10.24-25.088-10.24s-18.432 3.584-25.088 10.24c-6.656 6.656-10.752 15.872-10.752 25.088z" p-id="1740"></path></svg>
                  <div v-else-if="content.type === 'text'" class="text-content" style="width:80px;height:80px; display:flex; flex-direction:column; justify-content:center; align-items:center;">
                    <div style="font-size: 16px;">文字内容</div>
                    <div style="font-size: 13px; color: #666;">多行文本示例</div>
                  </div>
                </div>
              </BorderProgress>
              <div style="margin-top: 10px; font-size: 12px;">{{ content.type === 'image' ? '图片内容' : content.type === 'text' ? '文字内容' : '数字内容' }}</div>
            </div>
          </div>
        </div>
        <div class="info">支持任意插槽内容</div>
      </div>

      <!-- 示例 9：组件介绍 -->
      <div class="example">
        <h3>组件介绍</h3>
        <h4>基于Vue3 + TypeScript开发</h4>
        <div class="app-container" style="min-height: 200px;">
          <div style="display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: left; padding: 0 20px; width: 100%;">
            <div style="font-size: 14px; color: #333; line-height: 1.6; margin-bottom: 15px;">
              一个 Vue 3 边框进度条组件，带有光点动画效果，类似新能源车充电效果。
            </div>
            <div style="width: 100%;">
              <div style="font-size: 14px; color: #333; font-weight: 500; margin-bottom: 10px;">特性：</div>
              <ul style="font-size: 13px; color: #666; line-height: 1.8; padding-left: 2px; margin: 0;list-style-type: none;">
                <li>✨ 精美的边框进度条，沿着边框顺时针移动</li>
                <li>🎯 支持自适应内容尺寸或指定固定尺寸</li>
                <li>💫 光点动画效果，类似新能源车充电</li>
                <li>🌈 进度条和背景都有呼吸发光动画</li>
                <li>📦 TypeScript 支持</li>
                <li>🎨 高度可定制的样式和颜色</li>
                <li>📱 响应式设计，自动监听内容尺寸变化</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onUnmounted } from 'vue'
import BorderProgress from 'vue3-border-progressbar'

// 示例 1：基础用法
const progress1 = ref(50)
const updateProgress1 = () => {
  progress1.value = Math.floor(Math.random() * 100)
}

// 示例 2：不同进度值
const progressValues = [0, 25, 50, 75, 100]

// 示例 3：自定义尺寸
const sizes = [
  { width: 150, height: 150, text: '150x150' },
  { width: 200, height: 200, text: '200x200' },
  { width: 0, height: 0, text: '自适应' }
]

// 示例 4：自定义颜色
const colors = [
  { progressColor: '#67C23A', backgroundColor: 'rgba(103, 194, 58, 0.1)', text: '绿色' },
  { progressColor: '#F56C6C', backgroundColor: 'rgba(245, 108, 108, 0.1)', text: '红色' },
  { progressColor: '#409EFF', backgroundColor: 'rgba(64, 158, 255, 0.1)', text: '蓝色' },
  { progressColor: '#909399', backgroundColor: 'rgba(144, 147, 153, 0.1)', text: '灰色' }
]

// 示例 5：边框宽度
const strokeWidths = [2, 4, 8]

// 示例 6：动画速度
const durationItems = [
  { duration: 100, progress: ref(70) },
  { duration: 300, progress: ref(80) }
]
const updateDurationProgress = (index: number) => {
  durationItems[index].progress.value = Math.floor(Math.random() * 100)
}

// 示例 7：内容类型
const contentTypes = [
  { type: 'image' },
  { type: 'text' },
]

// 示例 8：动态进度
const dynamicProgress = ref(0)
let progressInterval: number | null = null
let isRunning = false

const startProgress = () => {
  if (!isRunning) {
    isRunning = true
    progressInterval = window.setInterval(() => {
      dynamicProgress.value = (dynamicProgress.value + 1) % 100
    }, 50)
  }
}

const stopProgress = () => {
  isRunning = false
  if (progressInterval) {
    clearInterval(progressInterval)
    progressInterval = null
  }
}

onUnmounted(() => {
  stopProgress()
})
</script>

<style scoped>
.app {
  width: 100%;
  min-height: 100vh;
  padding: 30px 20px;
  background-color: #f5f7fa;
  box-sizing: border-box;
}

h1 {
  text-align: center;
  color: #333;
  margin-bottom: 40px;
  font-size: 28px;
  font-weight: 600;
}

.example-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
  max-width: 1400px;
  margin: 0 auto;
}

.example {
  padding: 20px;
  background: white;
  border-radius: 12px;
  box-shadow: 0 4px 16px rgba(0,0,0,0.08);
  text-align: center;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.example:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 24px rgba(0,0,0,0.12);
}

.example h3 {
  margin-top: 0;
  color: #333;
  margin-bottom: 10px;
  font-size: 18px;
  font-weight: 600;
}

.example h4 {
  margin: 5px 0 15px 0;
  color: #666;
  font-size: 14px;
  font-weight: normal;
  line-height: 1.4;
}

.controls {
  margin-top: 20px;
  display: flex;
  justify-content: center;
  gap: 12px;
  flex-wrap: wrap;
}

button {
  padding: 12px 24px;
  margin: 0;
  cursor: pointer;
  background: #409eff;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 15px;
  font-weight: 500;
  transition: all 0.3s ease;
  box-shadow: 0 2px 8px rgba(64, 158, 255, 0.3);
}

button:hover {
  background: #66b1ff;
  box-shadow: 0 4px 12px rgba(64, 158, 255, 0.4);
  transform: translateY(-1px);
}

button:active {
  transform: translateY(0);
  box-shadow: 0 2px 6px rgba(64, 158, 255, 0.3);
}

.app-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 150px;
  padding: 5px;
}

.info {
  margin-top: 15px;
  font-size: 13px;
  color: #999;
  line-height: 1.5;
}

.grid-item {
  margin: 15px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.content-demo {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 10px;
}

.content-demo img {
  max-width: 80%;
  border-radius: 4px;
}

.content-demo .text-content {
  padding: 5px;
  text-align: center;
}

/* 优化示例1（动态进度）的按钮间距 */
.example:nth-child(1) .controls {
  gap: 15px;
}

/* 优化内容区域的垂直间距 */
.content-demo > div {
  margin: 5px 0;
}
</style>