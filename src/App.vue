<template>
    <div>
        <the-header title="RememberMe"></the-header>
        <!-- <learning-resource v-for="res in storeResources" :key="res.id" :title="res.title" :description="res.description"
            :link="res.link"></learning-resource> -->
        <!-- <store-resources :resources="storeResources"></store-resources> -->
        <the-resources></the-resources>
    </div>
</template>
<script>
import TheHeader from './components/layouts/TheHeader.vue'
import TheResources from './components/learning-resources/TheResources.vue'
// import StoreResources from './components/learning-resources/StoreResources.vue'
export default {
    components: { TheHeader, TheResources },
}
</script>
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

* {
    box-sizing: border-box;
}

html {
    font-family: 'Roboto', sans-serif;
}

body {
    margin: 0;
}
</style>