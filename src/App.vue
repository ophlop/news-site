<template>
    <AppHeader />
    <AppNews/>
    <AppFooter />
</template>

<script>
import AppHeader from './components/AppHeader.vue'
import AppNews from './components/AppNews.vue'
import AppFooter from './components/AppFooter.vue'

export default {
  components: { AppHeader, AppNews, AppFooter }
}

</script>

<style>

</style>
