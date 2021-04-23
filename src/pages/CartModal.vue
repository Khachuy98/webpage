<template>
  <div class="modalcart">
    <b-modal id="modalshow" hide-footer size="xl">
      <div class="wrapmodal">
        <div class="container">
          <div class="bg0 p-t-60 p-b-30 p-lr-15-lg how-pos3-parent">
            <b-row>
              <b-col lg="6">
                <b-card
                  img-src="data:image/jpeg;base64,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"
                  img-alt="Image"
                  style="max-width: 20rem"
                >
                </b-card>
              </b-col>
              <b-col lg="6">
                <h3>Chelsea Boot</h3>
                <div class="price">
                  <b-badge  pill variant="light">$40.09</b-badge> <br/>
                  <b-badge pill variant="light">$20.05</b-badge>
                </div>

                <div class="choose">
                  <b-form-select
                    class="size"
                    v-model="selected"
                    :options="size"
                  ></b-form-select>
                  <b-form-select
                    class="color"
                    v-model="selecteds"
                    :options="color"
                  ></b-form-select>
                  <b-form-spinbutton
                    class="count"
                    id="demo-sb"
                    v-model="value"
                    min="1"
                    max="50"
                  ></b-form-spinbutton>
                  <div class="actions">
                  <b-button class="addtocart" pill variant="info" @click="addItemToCart(product)">Add to cart</b-button>
                  <!-- <b-button class="buynow" pill variant="info" @click="addItemToCart(product)">Buy now</b-button> -->
                  </div>
                </div>
                  <b-card-text>
                  Some quick example text to build on the card title and make up
                  the bulk of the card's content.
                </b-card-text>
              </b-col>
            </b-row>
          </div>
        </div>
      </div>
    </b-modal>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cart: [],
      value: 1,
      selected: null,
      size: [
        { value: null, text: "Choose size" },
        { value: "1", text: "Size 37" },
        { value: "2", text: "Size 38" },
        { value: "3", text: "Size 39" },
        { value: "4", text: "Size 40 " },
        { value: "5", text: "Size 41 " },
        { value: "6", text: "Size 42 " },
        { value: "7", text: "Size 43 " },
      ],
      selecteds: null,
      color: [
        { value: null, text: "Choose color" },
        { value: "a", text: "Black" },
        { value: "b", text: "White" },
        { value: "c", text: "Red" },
        { value: "d", text: "Blue" },
        { value: "e", text: "Orange" },
      ],
    };
  },
  methods: {
    addItemToCart(product){
      this.cart.push(product);
      console.log(this);
    }
  }
};
</script>

<style scoped>
.col-3 {
  -ms-flex: 0 0 25%;
  -webkit-box-flex: 0;
  flex: 0 0 25%;
  max-width: 25%;
  padding: 15px 10px;
}
.modal .modal-content .modal-body {
  padding-top: 24px;
  padding-right: 24px;
  padding-bottom: 16px;
  padding-left: 24px;
  line-height: 1.9;
  height: 600px;
}
.modal .modal-content {
  margin: 0px 20px;
}
.choose {
  padding: 10px 10px;
  margin: 10px 50px;
  width: 200px;
}
.size {
  margin: 10px;
}
.color {
  margin: 10px;
}
.count {
  margin: 10px;
}
.addtocart{
    margin: 10px 38px;
}
.actions{
    display: block;
}
.price{
  font-size: 24px;
}
</style>