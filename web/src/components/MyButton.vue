<!-- MyButton.vue -->
<template>
    <button class="custom-button" @click="navigateToService">订制服务</button>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { useRouter } from 'vue-router'

export default defineComponent({
  methods: {
    navigateToService () {
      const router = useRouter()
      // 在这里指定你要跳转的路径
      router.push('/job')
    }
  }
})
</script>

<style scoped>
/* 样式省略，保留 .custom-button 样式 */
.custom-button {
    background-color: #4CAF50;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    cursor: pointer;
    border: none;
    border-radius: 8px;
    box-shadow: 0 6px #999;
    transition-duration: 0.4s;
}

.custom-button:hover {
    background-color: #45a049;
    box-shadow: 0 4px #666;
    transform: translateY(-2px);
}

.custom-button:active {
    background-color: #3e8e41;
    box-shadow: 0 2px #666;
    transform: translateY(4px);
}
</style>
