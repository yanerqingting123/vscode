<template>
  <div class="news">
    <AwHeader class="news_header" ref="headRef"></AwHeader>
    <div class="box">
      <div class="news-banner">
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
          placeholder="请输入新闻关键词"
          :trigger-on-focus="false"
        >
          <template #prefix>
            <el-icon>
              <Search />
            </el-icon>
          </template>
          <template #default="{ item }">
            <router-link :to="'/news/'+item.news_path" target="_blank">
              <div class="name" v-html="item.news_title"></div>
              <span class="desc" v-html="item.news_desc"></span>
            </router-link>
          </template>
        </el-autocomplete>
      </div>
    </div>
    <AwFooter></AwFooter>
  </div>
</template>
<script lang="ts" setup>
import AwHeader from '@/components/public/Header.vue'
import AwFooter from '@/components/public/Footer.vue'
import HotNews from '@/components/HotNews.vue'
import NewsList from '@/components/NewsList.vue'
import { Search } from '@element-plus/icons-vue'
import { onBeforeMount, onMounted, ref } from 'vue'
import mainStore from '@/store'
import { onBeforeRouteLeave } from 'vue-router'
import { searchNewsList, getNewsList, getRecomNewsApi } from '@/apis/news'
type NewsItem = {
  id: string;
  name: string;
};
const headRef = ref()
const newsTabs = ref<NewsItem[]>([])
const newsItems = ref<Record<any, any>>({})
const pageInfo = ref<{
  activeName: string;
  pagenum: number;
  pagesize: number;
  selectDate: '';
}>({
  activeName: '1',
  // 当前页码
  pagenum: 1,
  // 当前每页显示多少条数据
  pagesize: 10,
  selectDate: ''
})
const singlePage = ref(false)
const recomNews = ref<Array<any>>([])
const selectDate = ref('')
const searchList = ref<Array<any>>([])
const timeout = ref()
const autocomplete = ref()
const autocompleteFlag = ref(false)
const hotNews = ref<Array<any>>([])
const searchNews = ref<any>()
onBeforeMount(() => {

  getNewsItems()
  getRecomNews()
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
})

async function querySearchAsync (queryString: string, cb: (list: Array<any>) => void) {
  searchList.value = []
  const { data: res } = await searchNewsList(queryString)
  searchList.value = res?.data?.list ?? []
  const newHtml = `<span style="color: #3370ff">${queryString}</span>`
  searchList.value.forEach((item) => {
    item.news_title = item.news_title.replace(queryString, newHtml)
    item.news_desc = item.news_desc.replace(queryString, newHtml)
    // item.news_desc = item.news_desc.replace(queryString, newHtml)
  })
  clearTimeout(timeout.value)
  timeout.value = setTimeout(() => {
    cb(searchList.value)
  }, 1000 * Math.random())
}

/**
 * 选项卡切换
 * @param tab
 * @param event
 */
function handleClick (tab: number | string, event: Event) {
  getNewsItems()
}

async function getNewsItems () {
  const { data: res } = await getNewsList(pageInfo.value)
  if (res.status !== 200) {
    newsItems.value = {}
  } else {
    newsItems.value = res.data
    if (newsItems.value.total <= newsItems.value.limit) {
      singlePage.value = true
    }
  }
}

function searchByDate (data: any) {
  getNewsItems()
}

async function getRecomNews () {
  const { data: res } = await getRecomNewsApi()
  if (res.status !== 200) {
    hotNews.value = []
  } else {
    recomNews.value = res.data.list
  }
}

onBeforeRouteLeave((to, from, next) => {
  if (from.name === 'News') {
    mainStore.commit('setNavDarkActive', {
      navDarkActive: false
    })
    mainStore.commit('setHeaderLogo', {
      headerLogoShow: false
    })
  }
  next()
})
</script>
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
  height: 690px;
  background-size: cover;
  text-align: center;
  padding-top: 70px;

  :deep(.el-autocomplete) {
    width: 46%;
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
}


:deep(.el-tabs__nav-wrap::after) {
  content: none;
}

.box-card {
  width: 480px;
}
</style>

<style lang="less">
@hover_color: #3370ff;

.my-autocomplete {
  width: 46%;
  left: 50% !important;
  transform: translateX(-50%);
  li {
    line-height: normal;
    padding: 7px;

    .name {
      text-overflow: ellipsis;
      overflow: hidden;
    }

    .desc {
      font-size: 12px;
      color: #b4b4b4;
    }

    &.highlighted {
      background: #edf6ff !important;
    }

    .highlighted .addr {
      color: #ddd;
    }
  }

  a {
    color: rgba(0, 0, 0, 1);
    //transition: color .3s;
    display: block;
    text-overflow: ellipsis;
    overflow: hidden;
  }

  a:hover {
    color: @hover_color;
  }
}

.el-autocomplete-suggestion li:hover {
  background-color: #edf6ff !important;
}
</style>
