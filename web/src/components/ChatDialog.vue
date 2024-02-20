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
                        <div class="text">  {{ message.text }}</div>
                        <div class="big-container">
                            <div class="function-container">
                                <div class="function-second-container">
                                    <img src="../assets/img/new_imgs/key.png"  class="robot">
                                    <div class="second-title">教学大纲建议</div>
                                </div>
                                <div style="margin-left: 15px; margin-right: 15px; line-height: 30px; color: rgb(100, 94, 94);">我想做一份教学设计，你能给我列一个大纲吗？</div>
                            </div>
                            <div class="function-container">
                                <div class="function-second-container">
                                    <img src="../assets/img/new_imgs/love.png"  class="robot">
                                    <div class="second-title">教学设计建议</div>
                                </div>
                                <div style="margin-left: 15px; margin-right: 15px; line-height: 30px; color: rgb(100, 94, 94);">我想做一份创意的教学设计，能给我一些建议吗？</div>
                            </div>
                        </div>
                        <div class="big-container">
                            <div class="function-container">
                                <div class="function-second-container">
                                    <img src="../assets/img/new_imgs/jiantou.png"  class="robot">
                                    <div class="second-title">逐字稿生成</div>
                                </div>
                                <div style="margin-left: 15px; margin-right: 15px; line-height: 30px; color: rgb(100, 94, 94);">我有一份教学设计，你能根据我的教学设计帮我生成逐字稿吗？</div>
                            </div>
                            <div class="function-container">
                                <div class="function-second-container">
                                    <img src="../assets/img/new_imgs/huojian.png"  class="robot">
                                    <div class="second-title">教学课件生成</div>
                                </div>
                                <div style="margin-left: 15px; margin-right: 15px; line-height: 30px; color: rgb(100, 94, 94);">我有一份教学设计，你能根据我的教学设计帮我生成教学课件吗？</div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div v-else class="placeholder">开始一次新的对话...</div>
            <!-- <div v-if="showInput" class="user-input">
                <textarea v-model="userMessage" placeholder="请输入您的需求..."></textarea>
                <button @click="submitMessage">提交</button>
            </div> -->
        </div>
        <div v-if="showInput" class="user-input">
                <textarea v-model="userMessage" placeholder="请输入您的需求..."></textarea>
                <button @click="submitMessage">提交</button>
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
        { text: '............', avatar: '../assets/img/new_imgs/robot.png' }
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
.big-container{
    display: flex;
}
.function-container{
    background-color: rgb(240, 248, 255);
    margin-top: 20px;
    padding-bottom: 15px;
    padding-top: 5px;
    width: 340px;
    border-radius: 12px;
    margin-left: 20px;
}
.function-second-container{
    background-color: aliceblue;
    display: flex;
}
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
.second-title{
    font-size: 18px;
    margin-top: 5px;
    margin-left: 10px;
    font-weight: bold;
    color: #474643;
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
    width: 750px;
    margin-left: 200px;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.3);
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
    margin-top: 50px;
    background: #fff;
    padding: 20px;
    width: 750px;
    border-radius: 10px;
    margin-left: 200px;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
    display: flex;
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
