<template>
  <div class="homelayout">
    <top-nav-home/>
    <cart-product/> 
    <home></home>
</div>
</template>
<script>
import Contact from '../pages/Contact.vue'
import Home from '../pages/Home.vue'
import About from '../pages/About.vue'
import MobileMenu from './MobileMenu.vue'
import CartModal from '../pages/CartModal.vue'
import CartProduct from '../pages/CartProduct'
  import BaseDropdown from '../components/BaseDropdown.vue'
import TopNavHome from './TopNavHome.vue'
export default {
  components: {
    Home,
    About,
    MobileMenu,
    Contact,
    CartModal,
    CartProduct,
    BaseDropdown,
    TopNavHome,
  },
  methods: {
        toggleSidebar () {
        if (this.$sidebar.showSidebar) {
        this.$sidebar.displaySidebar(false)
        }
      },
      onSlideStart(slide) {
        this.sliding = true
      },
      onSlideEnd(slide) {
        this.sliding = false
      }
  }
}
</script>

<style scoped>
body{
  position: relative;
}
  .search{
    margin: 30px 7px;
  }
    .topnav{
        background-color: rgb(164, 166, 168);
        display: block;
      
    }
    .mr-sm-2{
        border-radius: 12px;
    }
    .main-panel{
    background: #00000000;
    position: relative;
    float: right;
    width: calc(100% );
    min-height: 100%;
    }
    .cart-bt{
      margin: 10px 10px;
    }

</style>