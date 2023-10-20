<template>
  <div class="bg-slate-50	h-screen py-2">
    <van-cell-group>
      <van-cell title="朋友圈" icon="thumb-circle-o" is-link to="/moments"/>
    </van-cell-group>
  </div>
  <!-- tbbar -->
  <Tabbar></Tabbar>
</template>

<script setup>
import { ref } from 'vue'
import Tabbar from '@/components/Tabbar.vue'
</script>
