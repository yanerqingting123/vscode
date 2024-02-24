<template>
  <div class="news">
    <AwHeader class="news_header" ref="headRef"></AwHeader>
    <div class="box">
      <div class="news-banner">
        <div class="banner-left">
        </div>
        <div class="banner-right">
          <el-autocomplete
          class="search-input"
          popper-class="my-autocomplete"
          highlight-first-item
          v-model="searchNews"
          clearable
          ref="autocomplete"
          @focus="autocompleteFlag = true"
          @blur="autocompleteFlag = false"
          @clear="searchHandle"
          :fetch-suggestions="querySearchAsync"
          placeholder="检索课程、直播、学习资料"
          :trigger-on-focus="false"
        >
      </el-autocomplete>
      <p>
        热门搜索
      </p>
      <LI>人工智能    珍惜动物</LI>
      <LI>人文故事    vr技术</LI>
        </div>
      </div>
      <div class="news-body">
        <div class="banner-1">
            <div class="image-container1">
            </div>
          <div class="text-container">
            <h3><router-link to="/newsDetail" >汽车动力之旅：666</router-link></h3>
            <p>课程介绍：了解汽车动力核心，掌握机械、电气
              与环保知识，体验智能科技，探索汽车未来趋势。</p>
          </div>
        </div>
        <div class="banner-2">
          <div class="image-container2">
          </div>
          <div class="text-container">
            <h3>智能LED与机器人：888</h3>
            <p>课程介绍：带领6-12岁的小学生开展探索人工
              智能原理、智能LED及会唱歌的“机器人”课程。
            </p>
          </div>
        </div>
        <div class="banner-3">
          <div class="image-container3">
          </div>
          <div class="text-container">
            <h3>创意DIY：588</h3>
            <p>课程介绍：激发无限创意，掌握手工技巧，
              打造个性作品，享受创作乐趣。</p>
          </div>
        </div>
        <div class="banner-4">
          <div class="image-container4">
          </div>
          <div class="text-container">
            <h3>在名画里的中国故事：800</h3>
            <p>赏析经典画作，解读画中故事，感受中华
              历史文化魅力，启发艺术审美与创造力。</p>
          </div>
        </div>
      </div>
    </div>
    <AwFooter></AwFooter>
  </div>
</template>
<script lang="ts" setup>
import AwHeader from '@/components/public/Header.vue'
import AwFooter from '@/components/public/Footer.vue'
import CheckboxAndDropdown from '@/components/CheckboxAndDropdown.vue'

import mainStore from '@/store'
import { onBeforeRouteLeave } from 'vue-router'
import { computed, onBeforeMount, onMounted, onUnmounted, ref, reactive } from 'vue'
import { getJobListApi, getJobFilter } from '@/apis/job'

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

.news-banner {
  width: 100%;
  height: 200px;
  text-align: center;
  margin-top: 50px;
  margin-bottom: 50px;
  display: flex;
}

.banner-left{
  width: 60%;
  height: 100%;
  background: url(../assets/img/index/banner.png) 100% no-repeat;
  background-size: cover;
  margin-left: 5%;
}

.banner-right{
  width: 40%;
  height: 100%;

  :deep(.el-autocomplete) {
    width: 80%;
    float:center;
    .el-input__wrapper {
      border-radius: 30px;
    }
    .el-input {
      border-radius: 30px !important;
    }
    .el-input__inner {
      height: 46px;
      line-height: 46px;
      border-radius: 30px;
      box-shadow: 0 2px 4px rgb(0 0 0 / 12%), 0 0 6px rgb(0 0 0 / 4%);
    }
    .el-input__icon {
      line-height: 46px;
      font-size: 16px;
    }
  }

  p{
    color: gray;
    font-size: 18px;
    text-align: left;
    margin-left: 10%;
    margin-top: 25px;
}
LI{
  color: gray;
    font-size: 12px;
    text-align: left;
    margin-left: 10%;
    margin-top: 15px;
}
}



.news-body {
  width: 100%;
  height: 400px;
  text-align: center;
  margin-top: 50px;
  margin-bottom: 50px;
  display: flex;
}

.banner-1 {
  width: 20%;
  height: 400px;
  margin-bottom: 30px;
  margin-top: 30px;
  margin-left: 5%;
  margin-right: 5%;
  flex: 1;
  }

.banner-2 {
  width: 20%;
  height: 400px;
  margin-bottom: 30px;
  margin-top: 30px;
  margin-right: 5%;
  flex: 1;
}
.banner-3 {
  width: 20%;
  height: 400px;
  margin-bottom: 30px;
  margin-top: 30px;
  margin-right: 5%;
  flex: 1;

}
.banner-4 {
  width: 20%;
  height: 400px;
  margin-bottom: 30px;
  margin-top: 30px;
  margin-right: 5%;
  flex: 1;
}

.image-container1 {
  height: 60%; /* 上面图片容器占据60%的高度 */
  background-image: url('../assets/img/index/dingzhifuwu.png');
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;

}

.image-container2 {
  height: 60%; /* 上面图片容器占据60%的高度 */
  background-image: url('../assets/img/index/led.png');
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;

}

.image-container3 {
  height: 60%; /* 上面图片容器占据60%的高度 */
  background-image: url('../assets/img/index/diy.png');
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;

}

.image-container4 {
  height: 60%; /* 上面图片容器占据60%的高度 */
  background-image: url('../assets/img/index/gushi.png');
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;

}

.text-container {
  height: 40%; /* 下面文字容器占据40%的高度 */


  h3{
   color:#3370ff;
    font-size: 18px;
    text-align: left;
    margin-top: 15px;
}

  p{
    color: gray;
    text-align: left;
    margin-top: 15px;
}
}


</style>

<style lang="less">
@hover_color: #3370ff;
</style>
