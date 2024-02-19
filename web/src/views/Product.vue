<template>
  <div class="container">
    <AwHeader class="product_header"></AwHeader>
    <div class="main-container">
      <div class="sidebar">
      <!-- 侧边栏内容，可以根据需要添加具体内容 -->
      <!-- 例如，可以在这里放置链接、图标等 -->
        <button class="new-dialog">新建对话</button>
        <div class="search-box">
          <input type="text" placeholder="搜索历史记录">
        </div>
        <div class="history_container">
          <img src="../assets/img/new_imgs/robot.png"  class="robot">
          <div class="history">哈喽，这是一条历史记录...</div>
        </div>
        <div class="history_container">
          <img src="../assets/img/new_imgs/robot.png"  class="robot">
          <div class="history">哈喽，这是一条历史记录...</div>
        </div>
        <div class="history_container">
          <img src="../assets/img/new_imgs/robot.png"  class="robot">
          <div class="history">哈喽，这是一条历史记录...</div>
        </div>
        <div class="history_container">
          <img src="../assets/img/new_imgs/robot.png"  class="robot">
          <div class="history">哈喽，这是一条历史记录...</div>
        </div>
        <div class="history_container">
          <img src="../assets/img/new_imgs/robot.png"  class="robot">
          <div class="history">哈喽，这是一条历史记录...</div>
        </div>
        <div class="history_container">
          <img src="../assets/img/new_imgs/robot.png"  class="robot">
          <div class="history">哈喽，这是一条历史记录...</div>
        </div>
        <div class="history_container">
          <img src="../assets/img/new_imgs/robot.png"  class="robot">
          <div class="history">哈喽，这是一条历史记录...</div>
        </div>
        <div class="history_container">
          <img src="../assets/img/new_imgs/robot.png"  class="robot">
          <div class="history">哈喽，这是一条历史记录...</div>
        </div>
        <div class="history_container">
          <img src="../assets/img/new_imgs/robot.png"  class="robot">
          <div class="history">哈喽，这是一条历史记录...</div>
        </div>
      </div>

    </div>

  </div>
</template>
<script lang="ts" setup>
import AwHeader from '@/components/public/Header.vue'
import mainStore from '@/store'
import { computed, onBeforeMount, onMounted, onUnmounted, ref, watch } from 'vue'
import { getProductLit } from '@/apis/product'
import { onBeforeRouteLeave } from 'vue-router'
import ChatDialog from '@/components/ChatDialog.vue'

const loading = ref(false)
const products = ref<Record<string, string>[]>([])
const activeIndex = ref(0)
const transitionName = ref('')
const scrolling = ref(false)
const duration = ref(1000)

const item = computed(() => products.value[activeIndex.value] || {})
</script>
<style lang = "less" scoped>
.history_container{
  display: flex;
  align-items: center; /* 垂直居中对齐 */
}
.robot{
  margin-left: 25px;
  width: 30px;
  margin-top: 30px;
}
.history{
  margin-left: 15px;
  margin-top: 35px;
}
.container {
  display: flex;
  flex-direction: column;
  height: 100vh;
  /* 设置高度为视窗高度，让布局占据整个屏幕 */
  background-color: #dbe8ec;
}

.main-container {
  display: flex;
  overflow: hidden;
  background-color: #f2f9fd;
}

.sidebar {
  /* 样式定义，例如宽度、背景色等 */
  position: relative;
  width: 300px;
  height: 729px;
  background: linear-gradient(to bottom, #f5f3f9, #ceebff);
  box-shadow: 0px 0 10px rgba(0, 0, 0, 0.3);
  /* 其他样式属性根据需求添加 */
}

.new-dialog {
  margin-top: 80px;
  margin-left: 40px;
  color: #1534fa;
  border: 2px solid #b0cbdd;
  /* 设置边框宽度和颜色 */
  border-radius: 10px;
  padding: 10px 20px;
  /* 设置按钮内边距 */
  font-size: 16px;
  /* 设置字体大小 */
  cursor: pointer;
  /* 设置鼠标悬停样式 */
}

.search-box {
  margin-top: 32px;
  margin-left: 10px;
  display: flex;
  align-items: center;
  margin-left: 20px; /* 调整间距 */
}

input {
  width: 80%;
  padding: 8px;
  margin-right: 5px;
}

input::placeholder {
  color: #aaa;
  /* 默认颜色，可以根据需要调整 */
}

input:focus {
  color: #020202;
  /* 输入时的字体颜色 */
}

.search-icon {
  font-size: 20px;
  margin-right: 8px;
}

.move-up-leave-active {
  -webkit-animation: outUp .7s cubic-bezier(.66, 0, .34, 1);
  animation: outUp .7s cubic-bezier(.66, 0, .34, 1);
  -webkit-animation-fill-mode: forwards;
  animation-fill-mode: forwards;
  -ms-transform: scale(1);
  transform: scale(1);
}

.move-down-enter-active {
  -webkit-animation: inDown .7s cubic-bezier(.66, 0, .34, 1);
  animation: inDown .7s cubic-bezier(.66, 0, .34, 1);
  -webkit-animation-fill-mode: forwards;
  animation-fill-mode: forwards;
  -ms-transform: scale(.6);
  transform: scale(.6);
}

.move-up-enter-active,
.move-down-enter-active {
  .logo {
    -webkit-animation: slideUpIn30 .77s .4s;
    animation: slideUpIn30 .77s .4s;
  }

  h2 {
    -webkit-animation: slideUpIn150 .77s .4s;
    animation: slideUpIn150 .77s .4s;
  }

  .description {
    -webkit-animation: slideUpIn100px .77s .4s;
    animation: slideUpIn100px .77s .4s;
  }
}

@keyframes inUp {
  0% {
    transform: translateY(100%);
    opacity: 0;
  }

  60% {
    opacity: 0.1;
  }

  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes outUp {
  0% {
    transform: translateY(0);
    opacity: 1;
  }

  50% {
    opacity: 0.1;
  }

  100% {
    transform: translateY(-100%);
    opacity: 0;
  }
}

@keyframes inDown {
  0% {
    transform: translateY(-100%);
    opacity: 0;
  }

  60% {
    opacity: 0.1;
  }

  100% {
    transform: translateY(0);
    opacity: 1;
  }
}

@keyframes outDown {
  0% {
    transform: translateY(0);
    opacity: 1;
  }

  50% {
    opacity: 0.1;
  }

  100% {
    opacity: 0;
    transform: translateY(100%);
  }
}

@keyframes slideUpIn30 {
  0% {
    transform: translate3d(0, 30%, 0);
    visibility: hidden;
  }

  100% {
    transform: translateZ(0);
    visibility: visible;
  }
}

@keyframes slideUpIn150 {
  0% {
    transform: translate3d(0, 150%, 0);
    visibility: hidden;
  }

  100% {
    transform: translateZ(0);
    visibility: visible;
  }
}

@keyframes slideUpIn100px {
  0% {
    transform: translate3d(0, 100px, 0);
    visibility: hidden;
  }

  100% {
    transform: translateZ(0);
    visibility: visible;
  }
}</style>
