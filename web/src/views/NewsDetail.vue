<template>
  <div class="news">
    <AwHeader class="news_header" ref="headRef" />
    <div class="box">
      <div class="news-body">
        <div class="body">
          <div class="body-left"></div>
          <div class="body-right">
            <div class="right1">
              <div class="r1-2">
                <h2>汽车动力之旅</h2>
                <p>适用年龄：6-15岁</p>
                <p>涉及学科：机械工程、环境科学、计算机科学、设计与美学</p>
              </div>
            </div>
            <div class="right2">
              <h2>￥666起</h2>
            </div>
            <div class="right3">
              <div class="r3-1">
                <button class="my-button1">立即购买</button>  
              </div>
              <div class="r3-2">
                <button class="my-button2">加入购物车</button> 
              </div>
              <div class="r3-3">
              </div>
            </div>
          </div>
        </div>
      </div>

    </div>
    <AwFooter />
  </div>
</template>
<script lang="ts" setup>
import AwHeader from '@/components/public/Header.vue'
import AwFooter from '@/components/public/Footer.vue'
import CheckboxAndDropdown from '@/components/CheckboxAndDropdown.vue'
import mainStore from '@/store'
import { onBeforeRouteLeave } from 'vue-router'
import { computed, onBeforeMount, onMounted, onUnmounted, ref, reactive } from 'vue'


const jobCities = ref([])
const job_category_id_list = ref([])
const location_code_list = ref([])
const searchBarFixedTop = ref(false)
const searchKeyword = ref('')
const currentPage = ref(1)
const pageSize = ref(10)
const loading = ref(false)
const locationCodeProps = ref({
  label: 'name'
})
const singlePage = ref(false)
const checked = ref(false)
const scrollTop = ref(0)
const oldScrollTop = ref(0)

const queryFilter = computed(() => {
  return {
    job_category_id_list: job_category_id_list.value,
    location_code_list: location_code_list.value,
    keyword: searchKeyword.value,
    pagesize: pageSize.value,
    currentPage: currentPage.value
  }
})



onMounted(() => {
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
  window.addEventListener('scroll', scrollHandle)
})

onUnmounted(() => {
  window.removeEventListener('scroll', scrollHandle)
})

function scrollHandle () {
  scrollTop.value =
    document.documentElement.scrollTop || window.pageYOffset || document.body.scrollTop
  oldScrollTop.value = scrollTop.value
  if (scrollTop.value >= 350) {
    mainStore.commit('setHeaderShow', {
      headerShow: true
    })
  } else {
    mainStore.commit('setHeaderShow', {
      headerShow: false
    })
  }
  searchBarFixedTop.value = scrollTop.value >= 430
}

// 请求筛选条件

</script >
<style lang="less" scoped>
@hover_color: #3370ff;

* {
  margin: 0;
  padding: 0;
}
.news_header {
  background-color: rgba(255, 255, 255, 0.5);
  backdrop-filter: blur(10px);
  //border-bottom: 1px solid #eff0f1;
}

.box {
  padding-top: 60px;
  //background: url("../../assets/img/news/bg_02.jpg");
  //background-size: cover;
}

.news-body {
  width: 100%;
  height: 600px;
  margin-top: 5%;
  margin-bottom: 5%;
  background-color: lightblue;
  border: 1px solid gray;
  display: flex;
}

.body{
  width: 100%;
  margin:2%;
  background-color: white;
  margin-bottom: 6%;
  border: 1px solid gray;
  margin: 20px;
  display: flex;
}

.body-left{
  width: 50%;
  height: 80%;
  background: url(../assets/img/index/dingzhiwufu.png) 100% no-repeat;
  background-size: cover;
  margin-left: 5%;
  margin-right: 5%;
  margin-top: 2%;
  flex: 1;
}

.body-right{
  width: 50%;
  height: 80%;
  margin-left: 50px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;

.right1{
  width: 100%;
  height: 40%;
  display: flex;
  flex-direction: row;
  padding: 5px;
  justify-content: space-between;

  h2{
    color:black;
    font-size: 48px;
    text-align: left;
    margin-left: 5px;
    margin-top: 20px;
  }
  p{    
    color:gray;
    font-size: 20px;
    text-align: left;
    margin-left: 5px;
    margin-top: 15px;
  }
}
.r1-2{
  width: 80%;
  height: 100%;
}
.right2{
  width: 100%;
  height: 30%;

  h2{
    color:bisque;
    font-size: 52px;
    text-align: left;
    margin-top: 40px;
    margin-left: 20px;
  }
}
.right3{
  width: 100%;
  height: 30%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  padding-top: 25px;
  padding-bottom: 25px;
}

.r3-1{
  width: 40%;
  height: 70%;
  background-color:cadetblue;
  display: flex;  
  justify-content: center;  
  align-items: center; 
  .my-button1 {    
  display: inline-block; /* 确保按钮是内联块级元素 */ 
  font-size: 40px; /* 字体大小 */  
  color:white; /* 字体颜色 */ 
  justify-content: center; /* 水平居中 */  
  align-items: center; /* 垂直居中 */ 
  border: none; /* 无边框 */  
  border-radius: 5px; /* 边框圆角 */  
  cursor: pointer; /* 鼠标悬停时变为手形 */  
  /* 根据需要添加其他样式 */  
} 
}
.r3-2{
  width: 40%;
  height: 70%;
  background-color: aquamarine ;
  margin-left: 5%;
  display: flex;  
  justify-content: center;  
  align-items: center; 
  .my-button2 {    
  display: inline-block; /* 确保按钮是内联块级元素 */ 
  font-size: 40px; /* 字体大小 */  
  color:white; /* 字体颜色 */ 
  justify-content: center; /* 水平居中 */  
  align-items: center; /* 垂直居中 */ 
  border: none; /* 无边框 */  
  border-radius: 5px; /* 边框圆角 */  
  cursor: pointer; /* 鼠标悬停时变为手形 */  
  /* 根据需要添加其他样式 */  
}
}
.r3-3{
  width: 20%;
  height: 70%;
  margin-left: 5%;
  margin-right: 10%;
  background: url(../assets/img/news/shoucang.jpg) 1% no-repeat;
}

 
}

</style>

<style lang="less">
@hover_color: #3370ff;
</style>
