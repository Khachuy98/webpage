<template>
  <b-container fluid class="shopproduct">
    <div class="p-b-10">
      <h2 class="boild">Product Overview</h2>
      <div class="flex-w flex-sb-m p-b-52">
        <div class="flex-w flex-l-m filter-tope-group m-tb-10">
          <b-button
            variant="link"
            class="stext-106 cl6 hov1 bor3 trans-04 m-r-32 m-tb-5 buttonselect"
            data-filter="*"
          >
            All Products
          </b-button>
          <b-button
            variant="link"
            class="stext-106 cl6 hov1 bor3 trans-04 m-r-32 m-tb-5 buttonselect"
            data-filter="boot"
          >
            Boot
          </b-button>
          <b-button
            class="stext-106 cl6 hov1 bor3 trans-04 m-r-32 m-tb-5 buttonselect"
            data-filter="sneaker"
          >
            Sneaker
          </b-button>
          <b-button
            variant="link"
            class="stext-106 cl6 hov1 bor3 trans-04 m-r-32 m-tb-5 buttonselect"
            data-filter="oxford"
          >
            Oxford
          </b-button>
          <b-button
            variant="link"
            class="stext-106 cl6 hov1 bor3 trans-04 m-r-32 m-tb-5 buttonselect"
            data-filter="chelsea"
          >
            Chelsea Boot
          </b-button>
        </div>
        <div class="products">
         <b-row align-h="center">
            <b-col cols="3" class="place-list" v-for="product in products" :key="product.name">            
              <div>
                <b-badge class="sale" variant="danger">{{ product.sale }}</b-badge>
                <img :src="product.image" />
              </div>
              <div class="infopr">
                {{ product.cost }} <br/>
              <a href="#" class="showModal" v-b-modal.modalshow>QuickView</a>
              <p>{{ product.name }}</p>
              </div>
            </b-col>
          </b-row>
        </div>
      </div>
    </div>
    <top-nav-home/>
    <cart-modal/>
  </b-container>
</template>

<script>
import TopNavHome from '../layout/TopNavHome.vue';
import CartModal from './CartModal.vue';
export default {
  components: { CartModal, TopNavHome },
  data() {
 return {
      cart: [],
      products: [
        {
          sale: "20%",
          name: "Coverse",
          cost: "$0.09",
          image:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRHOFqGW97VDm4zIA5Y6nI_KoyvnPQIbNwnODNB7kb91uN7upfZILNrEQ-9j83lXsH3unYJ1pk&usqp=CAc",
        },
        {
          sale: "30%",
          name: "Coverse1",
          cost: "$0.09",
          image:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRHOFqGW97VDm4zIA5Y6nI_KoyvnPQIbNwnODNB7kb91uN7upfZILNrEQ-9j83lXsH3unYJ1pk&usqp=CAc",
        },
        {
          sale: "40%",
          name: "Coverse2",
          cost: "$0.09",
          image:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRHOFqGW97VDm4zIA5Y6nI_KoyvnPQIbNwnODNB7kb91uN7upfZILNrEQ-9j83lXsH3unYJ1pk&usqp=CAc",
        },
        {
          name: "Coverse3",
          cost: "$0.09",
          image:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRHOFqGW97VDm4zIA5Y6nI_KoyvnPQIbNwnODNB7kb91uN7upfZILNrEQ-9j83lXsH3unYJ1pk&usqp=CAc",
        },
        {
          name: "Coverse4",
          cost: "$0.09",
          image:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRHOFqGW97VDm4zIA5Y6nI_KoyvnPQIbNwnODNB7kb91uN7upfZILNrEQ-9j83lXsH3unYJ1pk&usqp=CAc",
        },
        {
          name: "Coverse5",
          cost: "$0.09",
          image:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRHOFqGW97VDm4zIA5Y6nI_KoyvnPQIbNwnODNB7kb91uN7upfZILNrEQ-9j83lXsH3unYJ1pk&usqp=CAc",
        },
        {
          name: "Coverse6",
          cost: "$0.09",
          image:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRHOFqGW97VDm4zIA5Y6nI_KoyvnPQIbNwnODNB7kb91uN7upfZILNrEQ-9j83lXsH3unYJ1pk&usqp=CAc",
        },
        {
          name: "Coverse7",
          cost: "$0.09",
          image:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRHOFqGW97VDm4zIA5Y6nI_KoyvnPQIbNwnODNB7kb91uN7upfZILNrEQ-9j83lXsH3unYJ1pk&usqp=CAc",
        },
      ],
    };
  },
  methods: {
    addItemToCart(product) {
      this.cart.push(product);
      console.log(this.cart);
    },
  },
};
</script>

<style scoped>
.buttonselect {
  color: black;
  background-color: white;
  border-color: white;
  padding: 10px 20px;
}
.buttonselect:hover {
  color: red;
}
.boild {
  font-weight: bolder;
  text-transform: uppercase;
  padding-bottom: 15px;
}
.isotope-grid {
  position: relative;
  height: 1717.38px;
}
.block2-pic hov-img0 {
  width: 300px;
  height: 300px;
}
.place-list img{
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}
.infopr{
  text-align: center;
}
.sale{
  float: right;
}
</style>