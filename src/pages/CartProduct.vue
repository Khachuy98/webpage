<template>
  <div id="shopping-cart">
     <b-modal id="viewcart" hide-footer size="xl" title="View Cart">
      <div class="wrapmodal">
        <b-table striped hover class="viewproduct" 
        :items="items"
        ></b-table>
        <b-button variant="outline-dark">Remove Item</b-button>
      </div>
    </b-modal>
  </div>
</template>

<script>
export default {
 data() {
      return {
        items: [
          { name: 'shirt', quantity: 'Dickerson', price: 'Macdonald', totalprice: '$15245' },
          { name: 'jacket', quantity: 'Dickerson', price: 'Macdonald', totalprice: '$15245' },
          { name: 'adidass', quantity: 'Dickerson', price: 'Macdonald', totalprice: '$15245' },
          { name: 'chelsea' , quantity: 'Dickerson', price: 'Macdonald', totalprice: '$15245' },
        ]
      } 
    },
};

</script>
