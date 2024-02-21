<template>
    <div class="wrap-block">
        <div class="content-blok service-block">
            <div class="servie-block">
                <div class="block-line"></div>
                <p class="service-info-title">先科硬科普新传</p>
                <p class="service-info-subtitle">用最先进的科技创新教育，筑牢未来科创人才的“童子功”</p>
                <!-- <div class="service-list">
                    <div class="service-title" v-for="(item, index) in serviceList" :key="index">
                        <div class="is-hover-shadow">
                            <div class="service-title-shadow ">
                                <img :src="item.path" alt="">
                            </div>
                        </div>
                        <p class="service-name">{{ item.description }}</p>
                    </div>
                </div> -->
                <img src="../assets/img/new_imgs/1.png"  class="service-img">
            </div>
            <button class="custom-button">订制服务</button>
        </div>
        <div class="content-blok service-idea">
            <div class="service-idea">
                <div class="idea-left">
                    <img :src="serviceIdeaImg[0].path" :alt="serviceIdeaImg[0].name">
                </div>
                <div class="idea-right">
                    <div class="block-line"></div>
                    <p class="idea-title">{{ serviceIdeaInfo.ideaTitle }}</p>
                    <p class="idea-subtitle">{{ serviceIdeaInfo.ideaSubTitle }}</p>
                    <img :src="serviceIdeaImg[1].path" :alt="serviceIdeaImg[1].name">
                    <p class="idea-desc">{{ serviceIdeaInfo.ideaDesc }}</p>
                    <router-link to="/news">
                        <el-button type="primary" round>了解更多</el-button>
                    </router-link>
                </div>
            </div>
        </div>
        <div class="content-blok service-case">
            <div class="service-case">
                <div class="block-line"></div>
                <p class="case-title">主营服务</p>
                <p class="case-subtitle">未来之星，由先科绽放。始终坚持坚持以孩子为中心，以科学为导向的经营理念</p>
                <div class="case-list">
                    <div class="case-info" v-for="(item, index) in caseList" :key="index">
                        <el-card :body-style="{ padding: '0px' }" shadow="hover">
                            <img :src="item.path" :alt="item.desc" class="service-img-class">
                        </el-card>
                        <el-progress :percentage="50" :show-text="false"></el-progress>
                        <p class="case-desc">{{ item.desc }}</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script lang="ts" setup name="">
import { onBeforeMount, onMounted, ref } from 'vue'
// 这里演示一下如何实现复杂类型的定义，使用ts接口继承
interface BaseItem {
    path: string;
}
interface ServiceItem extends BaseItem {
    description: string;
}
interface ImgItem extends BaseItem {
    name: string;
}
interface CaseItem extends BaseItem {
    desc: string;
}
// 其实不用这么复杂，只是演示而已
type InfoData = {
    ideaTitle: string;
    ideaSubTitle: string;
    ideaDesc: string;
}
const serviceList = ref<ServiceItem[]>([])
const serviceIdeaInfo = ref<InfoData>({
  ideaTitle: '服务理念',
  ideaSubTitle: 'SERVICE IDEA',
  ideaDesc: '专注打造“高质量、多学科融合、多应用场景的PBL+STEAM深度硬科普系列标准化课程”，通过线上线下渠道融合、跨学科、项目式的展馆研学课程，助力展陈公司、科技馆升级或重构展馆的内容与形式，为研学机构提供优质内容。'
})
const serviceIdeaImg = ref<ImgItem[]>([])
const caseList = ref<CaseItem[]>([])
const percentage = ref('50')
onBeforeMount(() => {
  serviceList.value = [
    {
      description: '大数据',
      path: require('../assets/img/index/bigData.webp')
    },
    {
      description: '智能多媒体',
      path: require('../assets/img/index/media.webp')
    },
    {
      description: '互联网',
      path: require('../assets/img/index/internet.webp')
    },
    {
      description: '云计算',
      path: require('../assets/img/index/cloud.webp')
    }
  ]
  serviceIdeaImg.value = [
    {
      name: 'lefImg',
      path: require('../assets/img/index/service1.png')
    },
    {
      name: 'rightImg',
      path: require('../assets/img/index/service2.png')
    }
  ]
  caseList.value = [
    {
      desc: '原创课程包',
      path: require('../assets/img/index/kechengbao.png')
    },
    {
      desc: '原创教具包',
      path: require('../assets/img/index/jiaojubao.png')
    },
    {
      desc: '课程文创IP',
      path: require('../assets/img/index/wenchuangip.png')
    },
    {
      desc: '定制课程及服务',
      path: require('../assets/img/index/dingzhifuwu.png')
    }
  ]
})
</script>
<style lang="less" scoped>
.service-img-class{
    width: 200px;
    margin-top: 10px;
    height: 200px;
}
 .custom-button {
            background-color: #8ec1fb; /* 绿色 */
            color: rgb(249, 247, 247); /* 文字颜色 */
            padding: 15px 32px; /* 内边距 */
            text-align: center; /* 文字居中 */
            text-decoration: none; /* 去掉下划线 */
            display: inline-block; /* 使其既有块级元素的特性，又有行内元素的特性 */
            font-size: 20px; /* 文字大小 */
            margin: 4px 2px; /* 外边距 */
            cursor: pointer; /* 鼠标悬停时为指针形状 */
            border: none; /* 去掉边框 */
            border-radius: 8px; /* 边角圆润 */
            box-shadow: 0 4px #999; /* 阴影效果 */
            transition-duration: 0.4s; /* 过渡动画 */
            margin-top: 20px;
        }
.service-img{
    margin-top: 25px;
    width: 800px;
}
.wrap-block {
    position: relative;
    padding-top: 54px;

    .content-block {
        position: relative;
        overflow: hidden;
    }
}

.service-block {
    max-width: 1440px;
    height: 700px;
    margin: 0 auto;
    text-align: center;
    overflow-x: hidden;

    .block-line {
        margin: 0 auto 12px;
        width: 24px;
        height: 4px;
        background-color: #3370ff;
        border-radius: 100px;
    }

    .service-info-title {
        font-weight: 700;
        font-size: 34px;
        position: relative;
        bottom: 2px;
        padding-top: 20px;
    }

    .service-info-subtitle {
        font-size: 20px;
        line-height: 1.5;
        color: #646a73;
        margin-top: 30px;
    }

    .service-list {
        display: flex;
        justify-content: space-evenly;
        text-align: center;
        margin: 70px auto 0 auto;
    }

    .service-title-shadow {
        width: 111px;
        height: 111px;
        border-radius: 50%;
        display: flex;
        justify-content: center;
        align-items: center;
        transition: .3s;
    }

    .service-title-shadow:hover {
        width: 111px;
        height: 111px;
        border-radius: 50%;
        transform: scale(1.05) translateY(-1px);
        box-shadow: 0 6px 20px 0 rgba(0, 0, 0, .15);
    }

    .service-name {
        margin-top: 30px;
        font-weight: 600;
        font-size: 20px;
    }
}

.service-idea {
    background-color: #F5F5F5;
    width: 100%;

    .service-idea {
        max-width: 1440px;
        overflow: hidden;
        display: flex;
    }

    .idea-left img {
        width: 600px;
    }

    .idea-right {
        height: 500px;
        width: calc(100%-600px);
        margin-left: 100px;
        padding-top: 50px;

        .block-line {
            margin: 0 0 12px 0;
            width: 24px;
            height: 4px;
            background-color: #3370ff;
            border-radius: 100px;
        }

        .idea-title {
            font-weight: 700;
            font-size: 32px;
            position: relative;
            bottom: 2px;
            //padding-top: 60px;
        }

        .idea-subtitle {
            font-size: 16px;
            line-height: 1.5;
            color: #646a73;
            margin-top: 10px;
        }

        img {
            width: 500px;
            height: 200px;
            object-fit: cover;
            margin-top: 40px;
            margin-bottom: 30px;
            padding: 10px;
            border: #d3dce6 2px dashed;
        }

        .idea-desc {
            display: -webkit-box;
            -webkit-box-orient: vertical;
            -webkit-line-clamp: 4;
            overflow: hidden;
            max-height: 88px;
            max-width: 550px;
            font-size: 14px;
            line-height: 30px;
            color: #646a73;
        }

        .el-button {
            margin-top: 40px;
        }
    }
}

.service-case {
    background-color: #FFFFFF;
    width: 100%;

    .service-case {
        max-width: 1440px;
        //height: 700px;
        overflow: hidden;
        margin: 0 auto;
        text-align: center;
        padding-top: 50px;

        .block-line {
            margin: 0 auto 12px;
            width: 24px;
            height: 4px;
            background-color: #3370ff;
            border-radius: 100px;
        }

        .case-title {
            font-weight: 700;
            font-size: 32px;
            position: relative;
            bottom: 2px;
            //padding-top: 60px;
        }

        .case-subtitle {
            font-size: 16px;
            line-height: 1.5;
            color: #646a73;
            margin-top: 10px;
        }

        .case-list {
            display: flex;
            justify-content: space-evenly;
        }

        .el-card {
            width: 247px;
            height: 217px;
            margin-top: 40px;
        }

        .el-progress {
            margin-top: 10px;
        }

        /deep/ .el-progress-bar__outer {
            height: 2px !important;
        }

        .case-desc {
            margin-top: 30px;
            margin-bottom: 60px;
            font-weight: 500;
            font-size: 14px;
        }
    }
}
</style>
