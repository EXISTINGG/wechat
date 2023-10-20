<template>
  <!-- 顶部 -->
  <span class="fixed w-full z-50" :class="data.showNavBar ? 'block' : 'hidden'">
    <van-nav-bar
      title="朋友圈"
      left-arrow
      class="!bg-slate-50"
      @click-left="onClickLeft"
      :style="{
        backgroundColor: `rgba(230, 230, 230,${data.bgOpacity}) !important`
      }"
    >
      <template #right>
        <van-icon name="photograph" size="18" />
      </template>
    </van-nav-bar>
  </span>

  <div class="relative h-40 w-ful">
    <!-- 背景图 -->
    <img
      src="../../assets/vue.svg"
      alt=""
      class="absolute w-full h-full object-cover"
    />
    <!-- 昵称，头像 -->
    <div class="absolute -bottom-4 right-4 flex">
      <text class="mr-2 text-black font-black">昵称</text>
      <img src="../../assets/vue.svg" alt="" />
    </div>
  </div>

  <div class="p-10">
    <MomentsItem v-for="item in commentItemList" :item="item"/>
  </div>
</template>

<script setup>
import { reactive, ref, onMounted, onBeforeUnmount } from 'vue'
import { useRouter } from 'vue-router'
import MomentsItem from '@/components/MomentsItem.vue'

const router = useRouter()

const data = reactive({
  showNavBar: false,
  bgOpacity: 0,
  scrollTop: 0
})

const commentItemList = ref([])

const onClickLeft = () => router.back()

const getScrollTop = () => {
  data.scrollTop = window.pageYOffset
  if (data.scrollTop > 50) {
    data.showNavBar = true

    // 根据被卷去的高度调整背景透明度
    data.bgOpacity = (data.scrollTop - 100) / 10
  } else {
    data.showNavBar = false
  }
}

const loadMontents = () => [
  {
    user: { name: '阳和', avatar: '../../static/img/avatar2.png' },
    title: '华仔真棒，新的一年继续努力',
    images: [
      '../../static/img/reward1.png',
      '../../static/img/reward2.png',
      '../../static/img/reward3.png',
      '../../static/img/reward4.png'
    ],
    timestr: '3 分钟前',
    showReplyPanel: false,
    share: {},
    thumbsup: ['Guo 封面', '源小神'],
    replies: [
      { user: 'Guo 封面', text: '你也喜欢华仔哈!!!' },
      { user: '喵仔 zsy', text: '华仔实至名归哈' }
    ]
  },
  {
    user: { name: '伟科大人', avatar: '../../static/img/avatar3.png' },
    title: '全面读书日',
    images: [],
    timestr: '50 分钟前',
    showReplyPanel: false,
    share: {
      img: 'http://coding.imweb.io/img/p3/transition-hover.jpg',
      text: '飘洋过海来看你'
    },
    thumbsup: ['阳和'],
    replies: []
  },
  {
    user: { name: '深圳周润发', avatar: '../../static/img/avatar4.png' },
    title: '很好的色彩',
    images: ['http://coding.imweb.io/img/default/k-2.jpg'],
    timestr: '一小时前',
    showReplyPanel: false,
    share: {},
    thumbsup: [],
    replies: []
  },
  {
    user: { name: '喵仔咖啡', avatar: '../../static/img/avatar5.png' },
    title: '以后的咖啡不敢浪费了',
    images: [],
    timestr: '2 小时前',
    showReplyPanel: false,
    share: {},
    thumbsup: [],
    replies: []
  }
]

onMounted(() => {
  window.addEventListener('scroll', getScrollTop)
  commentItemList.value = loadMontents()
  console.log(commentItemList.value)
})

onBeforeUnmount(() => window.removeEventListener('scroll', getScrollTop))
</script>
