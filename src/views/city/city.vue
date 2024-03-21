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
        <!-- 2.tab标签页的切换 -->
        <!-- tabActive默认索引,加上name属性即可作为标签的索引值 -->
        <van-tabs v-model:active="tabActive" color="#fff9854">
          <template v-for="(value, key, index) in allCities" :key="key">
            <van-tab :title="value.title" :name="key"></van-tab>
          </template>
        </van-tabs>
      </div>
  
      <!-- 切换栏对应数据（具体实现看IndexBar索引栏） -->
      <div class="content">
        <!-- group-data父传子 -->
        <!-- <city-group :group-data="currentGroup"/> -->
        <!-- 使用v-show优化渲染 -->
        <template v-for="(value, key, index) in allCities" :key="key">
          <city-group v-show="tabActive === key" :group-data="value"/>
        </template>
     </div>
    </div>
  </template>
  
  <script setup>
  import { computed, ref } from "vue";
  import { storeToRefs } from "pinia";
  import { useRouter } from "vue-router";
  import useCityStore from "@/stores/modules/city";
  import CityGroup from "./cpns/city-group.vue";
  
  const router = useRouter()
  
  // 搜索框功能
  const searchValue = ref("")
  const onCancel = () => {
    // 返回上一级
    router.back()
  }
  
  // tab切换
  const tabActive = ref(0)
  
  // 从pinia的Store中获取数据
  const cityStore = useCityStore()
  cityStore.fetchAllCitiesData()
  const { allCities } = storeToRefs(cityStore)
  
  // 目的: 获取选中标签后的数据
  // 1.获取正确的key: 将tabs中绑定的tabAction正确绑定
  // 2.根据key从allCities获取数据, 默认直接获取的数据不是响应式的, 所以必须包裹computed
  // const currentGroup = computed(() => allCities.value[tabActive.value])
  </script>
  
  <style lang="less" scoped>
  .city {
    .top {
      position: relative;
      z-index: 9;
    }
    // 局部滚动
    .content {
      height: calc(100vh - 98px);
      overflow-y: auto;
    }
  }
  </style>