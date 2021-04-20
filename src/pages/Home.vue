<template>
  <div class="main-panel">
    <top-nav-home/>
    <slide></slide>
    <card></card>
    <shop></shop>
    <content-footer-home></content-footer-home>
  </div>
</template>

<script>
  import Shop from './Shop.vue'
  import ContentFooterHome from '../components/Footer/ContentFooterHome.vue'
  import Slide from '../pages/Slide.vue'
  import Card from '../pages/Card.vue'
  import TopNavHome from '../layout/TopNavHome.vue'
export default {
  components: { 
    TopNavHome,   
    Shop,
    ContentFooterHome,
    Slide,
    Card,
    }
}
</script>

<style>

</style>