<template>
    <div class="dialog-container">
        <div class="dialog-content">
            <div v-if="messages.length">
                <div v-for="(message, index) in messages" :key="index" class="message">
                    <div>
                        <div class="img-container">
                            <img src="../assets/img/new_imgs/robot.png"  class="robot">
                            <div class="title">你好，我是先科硬科普新传</div>
                        </div>
                        <div class="font">我是你的智能伙伴，先科硬科普新传——创课神器</div>
                        <div class="font">我可以根据你的教学设计为你生成逐字稿，也能根据你的教学设计生成教学课件。</div>
                        <div class="text">{{ message.text }}</div>
                    </div>
                </div>
            </div>
            <div v-else class="placeholder">开始一次新的对话...</div>
            <div v-if="showInput" class="user-input">
                <textarea v-model="userMessage" placeholder="请输入您的需求..."></textarea>
                <button @click="submitMessage">提交</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  props: {
    showInput: Boolean
  },
  data () {
    return {
      userMessage: '',
      messages: [
        { text: '欢迎使用我们的项目，这里是功能介绍...hahah哈哈哈ahahha', avatar: '../assets/img/new_imgs/robot.png' }
      ]
    }
  },

  methods: {
    submitMessage () {
      if (this.userMessage.trim() !== '') {
        this.messages.push({ text: this.userMessage, avatar: 'user-avatar.jpg' });
        this.userMessage = ''
        this.$emit('userSubmit')
      }
    }
  }
}
</script>

<style scoped>
.font{
    margin-top: 5px;
    margin-left: 5px;
    color: #6c6c6c;
}
.title{
    font-size: 25px;
    margin-top: 5px;
    margin-left: 10px;
    font-weight: bold;
}
.img-container{
    display: flex;
}
.robot{
  margin-left: 0px;
  width: 40px;
  margin-top: 0px;
}
.dialog-container {
    width: 800px;
    margin: 20px auto;
}

.dialog-content {
    background: #fff;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.5);
}

.message {
    display: flex;
    align-items: center;
    margin-bottom: 10px;
}

.avatar {
    width: 30px;
    height: 30px;
    margin-right: 10px;
    border-radius: 50%;
}

.text {
    flex-grow: 1;
}

.placeholder {
    color: #999;
    text-align: center;
    margin-top: 10px;
}

.user-input {
    margin-top: 10px;
}

textarea {
    width: 100%;
    resize: none;
    padding: 5px;
    margin-bottom: 5px;
}

button {
    padding: 5px 10px;
    cursor: pointer;
}
</style>
