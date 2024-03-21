<template>
    <div class="home">
        <HomeNavBar></HomeNavBar>
        <div class="banner">
            <img src="@/assets/img/home/banner.webp" alt="">
        </div>
        <HomeSearchBox></HomeSearchBox>
        <HomeCategories></HomeCategories>
    </div>
</template>

<script setup>

import HomeNavBar from "./cpns/home-nav-bar.vue";
import HomeSearchBox from "./cpns/home-search-box.vue";
import useHomeStore from '@/stores/modules/home';
import HomeCategories from "./cpns/home-categories.vue";

// 热门建议
const homeStore = useHomeStore()
homeStore.fetchHotSuggestData()
homeStore.fetchCategoriesData()
</script>

<style lang="less" scoped>
.banner {
    img {
        width: 100%;
    }
}
</style>