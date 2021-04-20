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
       </b-navbar-nav>
      <b-collapse id="nav-collapse" is-nav> </b-collapse>
      <div class="wrap-icon">
        <!-- <b-form-group
          label-for="filter-input"
          label-cols-sm="3"
          label-align-sm="right"
          label-size="sm"
          class="mb-0"
        > -->
          <!-- <b-input-group size="sm">
            <b-form-input
              id="filter-input"
              v-model="filter"
              type="search"
              placeholder="Type to Search"
            ></b-form-input>
            <b-input-group-append>
              <b-button :disabled="!filter" @click="filter = ''">Clear</b-button>
            </b-input-group-append>
          </b-input-group>
        </b-form-group> -->
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
    .topnavhome{
        position: fixed;
        left: 0;
        top: 0;
        width: 100%;
        z-index: 1000;
        background-color: white;
    }
</style>