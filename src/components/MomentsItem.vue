<template>
  <div class="flex">
    <!-- 头像 -->
    <img src="../assets/vue.svg" alt="" class="h-10" />

    <div class="flex flex-col w-full ml-1 py-2">
      <!-- 昵称and标题 -->
      <div class="flex flex-col justify-around h-10">
        <span>{{item.user.name}}</span>
        <span>{{item.title}}</span>
      </div>
      <!-- 内容 -->
      <div class="flex flex-wrap my-2" >
        <img v-for="item in item.images" src="../assets/vue.svg" alt="../assets/vue.svg" class="w-1/4 mr-2 mb-2">
        <!-- share -->
        <div class="bg-slate-200 flex items-center w-full" v-if="item?.share?.text">
          <img src="../assets/vue.svg" alt="">
          <text>{{item.share.text}}</text>
        </div>
      </div>

      <!-- 几分钟前 -->
      <div class="flex justify-between items-center mb-2">
        <text class=" text-slate-400 text-xs">{{item.timestr}}</text>
        <van-popover v-model:show="showPopover" :show-arrow="false" placement="left" actions-direction="horizontal" theme="dark" :actions="actions" @select="onSelect">
          <template #reference>
            <van-icon name="comment"/>
          </template>
        </van-popover>
      </div>

      <!-- 点赞，评论内容 -->
      <div class="bg-slate-200 w-full flex flex-col">
        <div class="p-1 text-blue-500" v-show="item.thumbsup.length">
          <van-icon name="like-o" class="mr-1"/>
          <span v-for="item in item.thumbsup">{{ `${item}，` }}</span>
        </div>

        <div class="van-hairline--bottom !bg-slate-300 z-10 h-0.5" v-show="item.replies.length"></div>

        <div class="p-1 w-full" v-show="item.replies.length">
          <div v-for="item in item.replies" class=" w-full" style="word-wrap: break-word;">
            <div class="w-48">
              <text class="text-blue-500 float-left">{{ `${item.user}：` }}</text>
              {{ item.text }}
            </div>
          </div>
        </div>
      </div>

    </div>
  </div>

  <div class="van-hairline--bottom !bg-slate-300 h-0.5 my-3" ></div>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
  item: {
    type: Object,
    required: true
  }
})

const showPopover = ref(false)
const actions = [{ text: '赞', icon: 'like-o' }, { text: '评论',icon: 'comment-o' }]
const onSelect = (item) => console.log(item);

</script>
