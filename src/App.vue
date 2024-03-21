<script setup>
import { RouterLink, RouterView,useRoute } from 'vue-router'
import TabBar from "@/components/tab-bar/tab-bar.vue";

const route = useRoute()
</script>

<template>
  <div class="app">
    <RouterView />  
    <TabBar v-if="!route.meta.hideTabBar"></TabBar>
  </div>

</template>

<style scoped>

</style>
