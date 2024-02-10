<template>
    <!-- 聊天气泡组件，根据消息发送者显示不同的样式 -->
    <div class="['chat-bubble', { 'user': isUser, 'other-sender': !isUser }]">
        {{ message.content }}
    </div>
</template>

<script setup>
import { ref, defineProps } from 'vue'

const props = defineProps(['message'])

const isUser = ref(props.message.sender === 'user')
</script>

<style scoped>
.chat-bubble {
    max-width: 70%;
    margin: 8px;
    padding: 12px;
    border-radius: 8px;
    word-wrap: break-word;
}

.user {
    align-self: flex-end;
    background-color: #b3e0ff;
}

.other-sender {
    align-self: flex-start;
    /* 其他发送者消息放在左侧 */
    background-color: #e0e0e0;
    /* 其他发送者消息背景颜色 */
}

/* 其他样式根据实际情况添加 */
</style>
