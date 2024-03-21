<template>
    <div class="city top-page">
      <div class="top">
        <!-- 1.搜索框 -->
        <van-search
          v-model="searchValue"
          shape="round"
          placeholder="城市/区域/位置"
          show-action
          @cancel="onCancel"
        />
      </div>
    </div>
  </template>
  
  <script setup>
  import { computed, ref } from "vue";
  import { useRouter } from "vue-router";
 import { getCityAll } from "@/services";

  const router = useRouter()
  
    // 搜索框功能
    const searchValue = ref("")
    const onCancel = () => {
      // 返回上一级
      router.back()
    }

    getCityAll().then(res => {
      console.log(res);
    })
  </script>