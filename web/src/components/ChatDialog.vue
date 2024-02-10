<template>
    <!-- 聊天对话框组件，显示聊天消息 -->
    <div class="chat-dialog">
        <!-- 使用 ChatBubble 组件渲染每一条消息 -->
        <ChatBubble v-for="message in messages" :key="message.id" :message="message" />
        <!-- 输入框用于发送消息 -->
        <input v-model="newMessage" @keyup.enter="sendMessage" placeholder="Type your message..." />
    </div>
</template>

<script setup>
import ChatBubble from '@/components/ChatBubble.vue' // 引入 ChatBubble 组件
import { ref } from 'vue'

// props
// eslint-disable-next-line no-undef
const { messages } = toRefs(defineProps(['messages']))

// state
const newMessage = ref('')

// methods
// const sendMessage = () => {
// // 创建新消息对象，这里假设消息的结构包括 id、content、sender 等属性
//   const message = {
//     id: generateUniqueId(),
//     content: newMessage.value,
//     sender: 'user'// 暂时假设消息由用户发送
//   },
//   // 将新消息添加到消息列表中
//   messages.value.push(message)
//   // 清空输入框
//   newMessage.value = '';
// };

// 生成唯一的消息 ID，这里可以使用更复杂的逻辑
// const generateUniqueId = () => {
//     return '_' + Math.random().toString(36).substr(2, 9);
// };
</script>

<style scoped>
/* 聊天对话框样式，样式可能需要根据实际情况调整 */
.chat-dialog {
    display: flex;
    flex-direction: column;
    padding: 20px;
    background-color: #ffffff;
    border: 1px solid #e0e0e0;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

/* 输入框样式，样式可能需要根据实际情况调整 */
input {
    margin-top: 12px;
    padding: 10px;
    border: 1px solid #e0e0e0;
    border-radius: 4px;
}
</style>
