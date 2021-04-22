<template>
  <div class="topnavhome">
    <b-navbar class="topnavbar" toggleable="lg" type="dark">
      <b-navbar-brand href="#">SHOES STORE</b-navbar-brand>
      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
        <b-navbar-nav >
          <router-link class="item-menu" to='/home'>Home</router-link>
          <router-link class="item-menu" to='/shop'>Shop</router-link>
          <router-link class="item-menu" to='/about'>About</router-link>
          <router-link class="item-menu" to='/contact'>Contact</router-link>
          <router-link class="item-cart" to='/viewcart'>View Cart</router-link>
       </b-navbar-nav>
      <b-collapse id="nav-collapse" is-nav> </b-collapse>
      <div class="wrap-icon">
        <b-button class="cart-bt">
          <b-icon icon="cart4" aria-hidden="true" v>Cart</b-icon>
        </b-button>
      </div>
    </b-navbar>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
    .item-menu{
      margin-left: 30px;
      color: black;

    }
    .item-menu :hover{
        color: #6c7ae0;
    }
    .item-cart{
      float: right;
    }
    .topnavhome{
        position: fixed;
        left: 0;
        top: 0;
        width: 100%;
        z-index: 1000;
        background-color: white;
    }
</style>