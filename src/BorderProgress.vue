<!--
  BorderProgress 组件 - 边框进度条组件

  功能说明：
  - 在内容周围显示一个矩形边框进度条
  - 进度条沿着边框顺时针方向移动（上→右→下→左）
  - 支持自适应内容尺寸或指定固定尺寸
  - 带有光点动画效果，类似新能源车充电效果
  - 进度条和背景都有呼吸发光动画

  使用示例：
  <BorderProgress :progress="50" :stroke-width="4" :padding="10">
    <img src="@/assets/imgs/logo.png" alt="logo" />
  </BorderProgress>

  参数说明：
  - progress: number (必填)
    进度值，范围 0-100
    示例：:progress="50"

  - width: number (可选，默认: 0)
    容器宽度，如果不设置则自适应内容宽度
    示例：:width="200"

  - height: number (可选，默认: 0)
    容器高度，如果不设置则自适应内容高度
    示例：:height="200"

  - strokeWidth: number (可选，默认: 4)
    边框线条宽度，单位：像素
    示例：:stroke-width="6"

  - progressColor: string (可选，默认: '#67C23A')
    进度条颜色，支持任何 CSS 颜色值
    示例：progress-color="#409eff"

  - backgroundColor: string (可选，默认: 'rgba(0, 0, 0, 0.1)')
    背景边框颜色，支持任何 CSS 颜色值
    示例：background-color="rgba(255, 0, 0, 0.2)"

  - animationDuration: number (可选，默认: 300)
    进度条动画持续时间，单位：毫秒
    示例：:animation-duration="500"

  插槽：
  - default: 默认插槽
    放置在进度条内部的内容
    示例：<img src="logo.png" /> 或 <div>内容</div>

  注意事项：
  1. 进度条边缘距离内容边缘固定为 1 像素
  2. 当进度为 0 或 100 时，光点不显示
  3. 组件使用 ResizeObserver 监听内容尺寸变化
  4. SVG 尺寸会自动计算，确保不会出现负值
-->
<template>
  <div class="border-progress-wrapper" ref="wrapperRef" :style="wrapperStyle">
    <svg
      v-if="svgWidth > 0 && svgHeight > 0"
      class="border-progress-svg"
      :width="svgWidth"
      :height="svgHeight"
      :viewBox="`0 0 ${svgWidth} ${svgHeight}`"
    >
      <!-- 背景边框 -->
      <path
        class="background-path"
        :d="pathD"
        :stroke="backgroundColor"
        :stroke-width="strokeWidth"
        fill="none"
        stroke-linecap="round"
        stroke-linejoin="round"
      />
      <!-- 进度边框 - 分为四条边 -->
      <path
        v-if="progress >= 0"
        class="progress-path-top"
        :d="topPathD"
        :stroke="progressColor"
        :stroke-width="strokeWidth"
        fill="none"
        stroke-linecap="round"
        stroke-linejoin="round"
        :stroke-dasharray="topDashArray"
        :stroke-dashoffset="topDashOffset"
      />
      <path
        v-if="progress > topRange.end"
        class="progress-path-right"
        :d="rightPathD"
        :stroke="progressColor"
        :stroke-width="strokeWidth"
        fill="none"
        stroke-linecap="round"
        stroke-linejoin="round"
        :stroke-dasharray="rightDashArray"
        :stroke-dashoffset="rightDashOffset"
      />
      <path
        v-if="progress > rightRange.end"
        class="progress-path-bottom"
        :d="bottomPathD"
        :stroke="progressColor"
        :stroke-width="strokeWidth"
        fill="none"
        stroke-linecap="round"
        stroke-linejoin="round"
        :stroke-dasharray="bottomDashArray"
        :stroke-dashoffset="bottomDashOffset"
      />
      <path
        v-if="progress > bottomRange.end"
        class="progress-path-left"
        :d="leftPathD"
        :stroke="progressColor"
        :stroke-width="strokeWidth"
        fill="none"
        stroke-linecap="round"
        stroke-linejoin="round"
        :stroke-dasharray="leftDashArray"
        :stroke-dashoffset="leftDashOffset"
      />
      <!-- 光点效果 -->
      <circle
        v-if="progress > 0 && progress < 100"
        class="light-point"
        :cx="lightPoint.x"
        :cy="lightPoint.y"
        :r="strokeWidth / 2 + 2"
        :fill="progressColor"
      />
    </svg>
    <div class="border-progress-content" ref="contentRef">
      <slot></slot>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed, ref, onMounted, onUnmounted, nextTick } from 'vue'

interface Props {
  progress: number // 进度 0-100
  width?: number // 容器宽度（可选，如果不设置则自适应）
  height?: number // 容器高度（可选，如果不设置则自适应）
  strokeWidth?: number // 边框宽度
  progressColor?: string // 进度条颜色
  backgroundColor?: string // 背景边框颜色
  animationDuration?: number // 动画持续时间(毫秒)
}

const props = withDefaults(defineProps<Props>(), {
  width: 0,
  height: 0,
  strokeWidth: 4,
  progressColor: '#67C23A', // 默认绿色
  backgroundColor: 'rgba(0, 0, 0, 0.1)',
  animationDuration: 300
})

const wrapperRef = ref<HTMLElement | null>(null)
const contentRef = ref<HTMLElement | null>(null)
const contentSize = ref({ width: 0, height: 0 })

// 监听内容大小变化
const updateContentSize = () => {
  if (contentRef.value) {
    contentSize.value = {
      width: contentRef.value.offsetWidth,
      height: contentRef.value.offsetHeight
    }
  }
}

onMounted(() => {
  nextTick(() => {
    updateContentSize()
  })
  // 监听内容变化
  if (typeof ResizeObserver !== 'undefined') {
    const resizeObserver = new ResizeObserver(() => {
      updateContentSize()
    })
    if (contentRef.value) {
      resizeObserver.observe(contentRef.value)
    }
    onUnmounted(() => {
      resizeObserver.disconnect()
    })
  }
})

// 实际宽度：如果设置了width则使用，否则使用内容宽度
const actualWidth = computed(() => {
  return props.width > 0 ? props.width : contentSize.value.width
})

// 实际高度：如果设置了height则使用，否则使用内容高度
const actualHeight = computed(() => {
  return props.height > 0 ? props.height : contentSize.value.height
})

// 容器样式
const wrapperStyle = computed(() => {
  const style: Record<string, string> = {}
  if (props.width > 0) {
    style.width = `${props.width}px`
  }
  if (props.height > 0) {
    style.height = `${props.height}px`
  }
  return style
})

// 内边距：进度条边缘与内容边缘之间的间距
const padding = 1

// SVG尺寸：内容尺寸 - 2*padding
// 这样SVG的viewBox就是从0到(内容尺寸-2*padding)
const svgWidth = computed(() => Math.max(0, actualWidth.value - padding * 2))
const svgHeight = computed(() => Math.max(0, actualHeight.value - padding * 2))

// 计算边框坐标
// 进度条中心线距离SVG边缘的距离 = padding + strokeWidth/2
const coords = computed(() => {
  const halfStroke = props.strokeWidth / 2
  const offset = padding + halfStroke // 进度条中心线距离SVG边缘的距离
  const size = svgWidth.value - halfStroke * 2 // 进度条路径矩形的宽高

  return {
    x: offset,
    y: offset,
    w: size,
    h: size
  }
})

// 背景路径
const pathD = computed(() => {
  const { x, y, w, h } = coords.value
  return `M ${x} ${y} L ${x + w} ${y} L ${x + w} ${y + h} L ${x} ${y + h} Z`
})

// 上边路径（0-25%）
const topPathD = computed(() => {
  const { x, y, w } = coords.value
  return `M ${x} ${y} L ${x + w} ${y}`
})

// 右边路径（25-50%）
const rightPathD = computed(() => {
  const { x, y, w, h } = coords.value
  return `M ${x + w} ${y} L ${x + w} ${y + h}`
})

// 下边路径（50-75%）
const bottomPathD = computed(() => {
  const { x, y, w, h } = coords.value
  return `M ${x + w} ${y + h} L ${x} ${y + h}`
})

// 左边路径（75-100%）
const leftPathD = computed(() => {
  const { x, y, h } = coords.value
  return `M ${x} ${y + h} L ${x} ${y}`
})

// 计算每条边的长度
const topLength = computed(() => coords.value.w)
const rightLength = computed(() => coords.value.h)
const bottomLength = computed(() => coords.value.w)
const leftLength = computed(() => coords.value.h)

// 计算周长
const perimeter = computed(() => 2 * (coords.value.w + coords.value.h))

// 计算每条边在周长中的占比
const topRatio = computed(() => topLength.value / perimeter.value)
const rightRatio = computed(() => rightLength.value / perimeter.value)
const bottomRatio = computed(() => bottomLength.value / perimeter.value)
const leftRatio = computed(() => leftLength.value / perimeter.value)

// 计算每条边的进度百分比范围（0-100）
const topRange = computed(() => ({
  start: 0,
  end: topRatio.value * 100
}))

const rightRange = computed(() => ({
  start: topRange.value.end,
  end: topRange.value.end + rightRatio.value * 100
}))

const bottomRange = computed(() => ({
  start: rightRange.value.end,
  end: rightRange.value.end + bottomRatio.value * 100
}))

const leftRange = computed(() => ({
  start: bottomRange.value.end,
  end: 100
}))

// 计算每条边的进度（0-1）
const topProgress = computed(() => {
  if (props.progress <= topRange.value.start) return 0
  if (props.progress >= topRange.value.end) return 1
  const range = topRange.value.end - topRange.value.start
  return (props.progress - topRange.value.start) / range
})

const rightProgress = computed(() => {
  if (props.progress <= rightRange.value.start) return 0
  if (props.progress >= rightRange.value.end) return 1
  const range = rightRange.value.end - rightRange.value.start
  return (props.progress - rightRange.value.start) / range
})

const bottomProgress = computed(() => {
  if (props.progress <= bottomRange.value.start) return 0
  if (props.progress >= bottomRange.value.end) return 1
  const range = bottomRange.value.end - bottomRange.value.start
  return (props.progress - bottomRange.value.start) / range
})

const leftProgress = computed(() => {
  if (props.progress <= leftRange.value.start) return 0
  if (props.progress >= leftRange.value.end) return 1
  const range = leftRange.value.end - leftRange.value.start
  return (props.progress - leftRange.value.start) / range
})

// 计算每条边的dasharray和dashoffset
const topDashArray = computed(() => `${topLength.value}`)
const topDashOffset = computed(() => topLength.value * (1 - topProgress.value))

const rightDashArray = computed(() => `${rightLength.value}`)
const rightDashOffset = computed(() => rightLength.value * (1 - rightProgress.value))

const bottomDashArray = computed(() => `${bottomLength.value}`)
const bottomDashOffset = computed(() => bottomLength.value * (1 - bottomProgress.value))

const leftDashArray = computed(() => `${leftLength.value}`)
const leftDashOffset = computed(() => leftLength.value * (1 - leftProgress.value))

// 计算光点位置
const lightPoint = computed(() => {
  const { x, y, w, h } = coords.value
  const p = props.progress

  // 上边：0-25%
  if (p <= topRange.value.end) {
    const progress = p / topRange.value.end
    return {
      x: x + w * progress,
      y: y
    }
  }

  // 右边：25-50%
  if (p <= rightRange.value.end) {
    const progress = (p - rightRange.value.start) / (rightRange.value.end - rightRange.value.start)
    return {
      x: x + w,
      y: y + h * progress
    }
  }

  // 下边：50-75%
  if (p <= bottomRange.value.end) {
    const progress = (p - bottomRange.value.start) / (bottomRange.value.end - bottomRange.value.start)
    return {
      x: x + w - w * progress,
      y: y + h
    }
  }

  // 左边：75-100%
  const progress = (p - leftRange.value.start) / (leftRange.value.end - leftRange.value.start)
  return {
    x: x,
    y: y + h - h * progress
  }
})
</script>

<style scoped>
.border-progress-wrapper {
  position: relative;
  display: inline-block;
}

.border-progress-svg {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  pointer-events: none;
  z-index: 1;
}

.background-path {
  filter: drop-shadow(0 0 2px rgba(0, 0, 0, 0.1));
  animation: backgroundPulse 3s ease-in-out infinite;
}

.progress-path-top,
.progress-path-right,
.progress-path-bottom,
.progress-path-left {
  transform-box: fill-box;
  transform-origin: center;
  transition: stroke-dashoffset v-bind(animationDuration + 'ms') ease-out;
  filter: drop-shadow(0 0 4px currentColor);
  animation: progressGlow 2s ease-in-out infinite;
}

@keyframes backgroundPulse {
  0%, 100% {
    opacity: 0.3;
  }
  50% {
    opacity: 0.5;
  }
}

@keyframes progressGlow {
  0%, 100% {
    filter: drop-shadow(0 0 4px currentColor);
  }
  50% {
    filter: drop-shadow(0 0 8px currentColor);
  }
}

.light-point {
  filter: drop-shadow(0 0 6px currentColor) drop-shadow(0 0 12px currentColor);
  animation: pointPulse 1.5s ease-in-out infinite;
}

@keyframes pointPulse {
  0%, 100% {
    opacity: 0.8;
    transform: scale(1);
  }
  50% {
    opacity: 1;
    transform: scale(1.2);
  }
}

.border-progress-content {
  position: relative;
  z-index: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  box-sizing: border-box;
}
</style>
