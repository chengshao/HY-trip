<template>
    <div class="city-group">
      <van-index-bar :index-list="indexList">
        <van-index-anchor index="热门"/>
        <div class="list">
          <template v-for="(city, index) in groupData.hotCities">
            <div class="city" @click="cityClick(city)">{{ city.cityName }}</div>
          </template>
        </div>
  
        <template v-for="(group, index) in groupData?.cities" :key="index">
          <van-index-anchor :index="group.group" />
          <template v-for="(city, indey) in group.cities" :key="indey">
            <van-cell :title="city.cityName" @click="cityClick(city)"/>
          </template>
      </template>
      </van-index-bar>
    </div>
  </template>
  
  <script setup>
  import { computed, ref } from "vue";
  import useCityStore from "@/stores/modules/city";
  import { useRouter } from "vue-router";

  // 从city.vue传参数到city-group.vue
  const props = defineProps({
    groupData: {
      type: Object,
      default: () => ({})
    }
  })
  
  // 城市列表索引动态映射
  const indexList = computed(() => {
    const list = props.groupData.cities.map(item => item.group)
    // 在list最前面插入一个#，给热门添加索引
    list.unshift("#")
    return list
  })
  // ....
  // 监听城市点击
  const router = useRouter()
  const cityStore = useCityStore()
  const cityClick = (city) => {
    // 选中当前城市
    cityStore.currentCity = city
    // 返回上一级
    router.back()
  }
  </script>
  
  <style lang="less" scoped>
  .list {
    display: flex;
    /* 换行 */
    flex-wrap: wrap;
    justify-content: space-around;
    padding: 10px;
    padding-right: 25px;
  
    .city {
      width: 70px;
      height: 28px;
      border-radius: 14px;
      font-size: 12px;
      color: #000;
      text-align: center;
      line-height: 28px;
      background-color: #fff4ec;
      margin: 6px 0;
    }
  }
  </style>