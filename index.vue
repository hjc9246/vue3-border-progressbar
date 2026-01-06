<template>
  <div class="border-progress-wrapper" :style="wrapperStyle">
    <svg class="border-progress-svg" :width="width" :height="height" :viewBox="`0 0 ${width} ${height}`">
      <!-- 背景边框 -->
      <rect
        :x="strokeWidth / 2"
        :y="strokeWidth / 2"
        :width="width - strokeWidth"
        :height="height - strokeWidth"
        :stroke="backgroundColor"
        :stroke-width="strokeWidth"
        fill="none"
        rx="4"
      />
      <!-- 进度边框 -->
      <rect
        class="progress-rect"
        :x="strokeWidth / 2"
        :y="strokeWidth / 2"
        :width="width - strokeWidth"
        :height="height - strokeWidth"
        :stroke="progressColor"
        :stroke-width="strokeWidth"
        fill="none"
        rx="4"
        :stroke-dasharray="totalDashArray"
        :stroke-dashoffset="dashOffset"
        :style="progressStyle"
      />
    </svg>
    <div class="border-progress-content">
      <slot></slot>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'

interface Props {
  progress: number // 进度 0-100
  width?: number // 容器宽度
  height?: number // 容器高度
  strokeWidth?: number // 边框宽度
  progressColor?: string // 进度条颜色
  backgroundColor?: string // 背景边框颜色
  animationDuration?: number // 动画持续时间(毫秒)
}

const props = withDefaults(defineProps<Props>(), {
  width: 100,
  height: 100,
  strokeWidth: 4,
  progressColor: '#67C23A', // 默认绿色
  backgroundColor: 'rgba(0, 0, 0, 0.1)',
  animationDuration: 300
})

// 计算边框总长度 (周长)
const perimeter = computed(() => {
  const w = props.width - props.strokeWidth
  const h = props.height - props.strokeWidth
  return 2 * (w + h)
})

// stroke-dasharray: [实线长度, 间隙长度]
const totalDashArray = computed(() => `${perimeter.value}`)

// stroke-dashoffset: 控制显示的进度
// offset = perimeter * (1 - progress / 100)
const dashOffset = computed(() => {
  const clampedProgress = Math.min(100, Math.max(0, props.progress))
  return perimeter.value * (1 - clampedProgress / 100)
})

const wrapperStyle = computed(() => ({
  width: `${props.width}px`,
  height: `${props.height}px`
}))

const progressStyle = computed(() => ({
  transition: `stroke-dashoffset ${props.animationDuration}ms ease-out`
}))
</script>

<style scoped>
.border-progress-wrapper {
  position: relative;
  display: inline-block;
}

.border-progress-svg {
  position: absolute;
  top: 0;
  left: 0;
  pointer-events: none;
  z-index: 1;
}

.progress-rect {
  transform-box: fill-box;
  transform-origin: center;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.border-progress-content {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  z-index: 0;
}
</style>
