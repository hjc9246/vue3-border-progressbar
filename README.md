# vue3-border-progressbar

一个 Vue 3 边框进度条组件，带有光点动画效果，类似新能源车充电效果。

## 特性

- ✨ 精美的边框进度条，沿着边框顺时针移动
- 🎯 支持自适应内容尺寸或指定固定尺寸
- 💫 光点动画效果，类似新能源车充电
- 🌈 进度条和背景都有呼吸发光动画
- 📦 TypeScript 支持
- 🎨 高度可定制的样式和颜色
- 📱 响应式设计，自动监听内容尺寸变化

## 效果展示

![效果展示](demo.gif)

## 安装

```bash
npm install vue3-border-progressbar
# 或
yarn add vue3-border-progressbar
# 或
pnpm add vue3-border-progressbar
```

## 使用

### 全局注册

```typescript
import { createApp } from 'vue'
import BorderProgress from 'vue3-border-progressbar'
import App from './App.vue'

const app = createApp(App)
app.use(BorderProgress)
app.mount('#app')
```

### 局部使用

```vue
<template>
  <BorderProgress :progress="50" :stroke-width="4">
    <img src="@/assets/logo.png" alt="logo" />
  </BorderProgress>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import BorderProgress from 'vue3-border-progressbar'

const progress = ref(50)
</script>
```

## API

### Props

| 参数 | 类型 | 默认值 | 必填 | 说明 |
|------|------|--------|------|------|
| progress | number | - | 是 | 进度值，范围 0-100 |
| width | number | 0 | 否 | 容器宽度，0 表示自适应内容宽度 |
| height | number | 0 | 否 | 容器高度，0 表示自适应内容高度 |
| strokeWidth | number | 4 | 否 | 边框线条宽度，单位：像素 |
| progressColor | string | '#67C23A' | 否 | 进度条颜色 |
| backgroundColor | string | 'rgba(0, 0, 0, 0.1)' | 否 | 背景边框颜色 |
| animationDuration | number | 300 | 否 | 进度条动画持续时间，单位：毫秒 |

## 示例

### 基础用法

```vue
<BorderProgress :progress="50">
  <div>内容</div>
</BorderProgress>
```

### 自定义尺寸

```vue
<BorderProgress :progress="75" :width="200" :height="200">
  <img src="logo.png" width="100" height="100" />
</BorderProgress>
```

### 自定义颜色

```vue
<BorderProgress
  :progress="60"
  progress-color="#409eff"
  background-color="rgba(64, 158, 255, 0.1)"
>
  <div>自定义颜色</div>
</BorderProgress>
```

### 自定义边框宽度

```vue
<BorderProgress :progress="80" :stroke-width="6">
  <div>粗边框</div>
</BorderProgress>
```

### 自定义动画时长

```vue
<BorderProgress :progress="90" :animation-duration="500">
  <div>慢速动画</div>
</BorderProgress>
```

## 浏览器支持

- Chrome >= 87
- Firefox >= 78
- Safari >= 14
- Edge >= 88

## License

MIT

## 作者

hjc9246 <hjc9246@gmail.com>

## 贡献

欢迎提交 Issue 和 Pull Request！
