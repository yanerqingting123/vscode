<template>
  <div class="container">
    <AwHeader class="product_header"></AwHeader>
    <div class="main-container">
      <div class="sidebar">
      <!-- 侧边栏内容，可以根据需要添加具体内容 -->
      <!-- 例如，可以在这里放置链接、图标等 -->
    </div>

    <!-- 主要内容容器 -->
    <div class="main-content">
      <!-- 主要内容，包括原有的产品展示部分 -->
      <!-- ... -->
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

const loading = ref(false)
const products = ref<Record<string, string>[]>([])
const activeIndex = ref(0)
const transitionName = ref('')
const scrolling = ref(false)
const duration = ref(1000)

const item = computed(() => products.value[activeIndex.value] || {})

watch(() => activeIndex.value, (newIndex, oldIndex) => {
  if (scrolling.value) {
    return
  }
  transitionName.value = newIndex < oldIndex ? 'move-down' : 'move-up'
})

// 挂载前
onBeforeMount(async () => {
  mainStore.commit('setHeaderLogo', {
    headerLogoShow: false
  })
  mainStore.commit('setShadowActive', {
    headerShadowActive: false
  })
  mainStore.commit('setNavDarkActive', {
    navDarkActive: true
  })
  mainStore.commit('setHeaderShow', {
    headerShow: false
  })
  loading.value = true
  const { data: res } = await getProductLit()
  if (res.status === 200) {
    products.value = res.data.list
    loading.value = false
  }
})
// 挂载完成
onMounted(() => {
  window.addEventListener('mousewheel', mousewheelHandler)
  window.addEventListener('DOMMouseScroll', mousewheelHandler)
})
// 卸载后
onUnmounted(() => {
  window.removeEventListener('mousewheel', mousewheelHandler)
  window.removeEventListener('DOMMouseScroll', mousewheelHandler)
})
function mousewheelHandler (e: Event) {
  if (scrolling.value) {
    return
  }
  scrolling.value = true
  // @ts-ignore
  if (e.wheelDelta > 0 || e.detail < 0) {
    transitionName.value = 'move-down'
    activeIndex.value =
      activeIndex.value === 0
        ? products.value.length - 1
        : activeIndex.value - 1
  } else {
    transitionName.value = 'move-up'
    activeIndex.value = (activeIndex.value + 1) % products.value.length
  }
  setTimeout(() => {
    scrolling.value = false
  }, duration.value)
}

onBeforeRouteLeave((to, from, next) => {
  if (from.name === 'Product') {
    mainStore.commit('setNavDarkActive', {
      navDarkActive: false
    })
    mainStore.commit('setHeaderLogo', {
      headerLogoShow: true
    })
    next()
  }
})
</script>
<style lang = "less" scoped>
.container{
  display: flex;
  flex-direction: column;
  height: 100vh; /* 设置高度为视窗高度，让布局占据整个屏幕 */
  background-color: #f2f8fa;
}

.main-container {
  display: flex;
}

.sidebar {
  /* 样式定义，例如宽度、背景色等 */
  width: 300px;
  height: 729px;
  background: linear-gradient(to bottom, #f5f3f9, #ceebff);
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
  /* 其他样式属性根据需求添加 */
}

.main-content {
  /* 样式定义，例如设置右边边距留出侧边栏空间 */
  flex: 1; /* 使用 flex 属性，使主要内容占据剩余空间 */
  padding: 20px; /* 为主要内容添加一些内边距 */
  background-color: #fefeff;
  /* 其他样式属性根据需求添加 */
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
}
</style>
