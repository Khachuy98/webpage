<template>
  <div class="content">
    <div class="container-fluid">
      <div class="row">
        <div class="col-12">
          <card
            class="strpied-tabled-with-hover"
            body-classes="table-full-width table-responsive"
          >
            <template slot="header">
              <h4 class="card-title">Product list</h4>
              <p class="card-category">Here is a product</p>
              <div class="text-center">
                <button
                  type="submit"
                  class="btn btn-info btn-fill float-right"
                  v-b-modal.add-product
                >
                  Add new
                </button>
              </div>
              <table class="table">
                <thead>
                  <slot name="columns">
                    <tr>
                      <th>ID</th>
                      <th>Name</th>
                      <th>Quantity</th>
                      <th>Image</th>
                      <th>Price</th>
                      <th>Status</th>
                      <th>Supplier</th>
                      <th>Action</th>
                    </tr>
                  </slot>
                </thead>
                <tbody>
                  <tr v-for="product in products.data" v-bind:key="product.id">
                    <td>{{ product.id }}</td>
                    <td>{{ product.name }}</td>
                    <td>{{ product.amount }}</td>
                    <td>{{ product.img }}</td>
                    <td>{{ product.export_price }}</td>
                    <td>{{ product.status }}</td>
                    <td>{{ product.supplier_id }}</td>
                    <td>
                      <a href="#" v-b-modal.modal-edit>
                        <i class="fa fa-eye"></i>
                      </a>
                      /
                      <a href="#" v-b-modal.modal-edit>
                        <i class="fa fa-edit"></i>
                      </a>
                      /
                      <a href="#" @click="clickDelete(item.id)">
                        <i class="fa fa-trash"></i>
                      </a>
                    </td>
                  </tr>
                </tbody>
                <b-modal
                  size="xl"
                  id="add-product"
                  ref="modal"
                  title="Add product"
                  @ok="handleOk"
                  @show="resetModal"
                  @hidden="resetModal"
                >
                  <form @submit.prevent="handleOk">
                    <b-row>
                      <b-col lg="5">
                        <b-form-group
                          label="Name"
                          label-for="name-input"
                          invalid-feedback="Name is required"
                        >
                          <b-form-input
                            id="name-input"
                            v-model="formadd.name"
                            required
                          ></b-form-input>
                        </b-form-group>
                        <b-form-file
                          v-model="formadd.img"
                          :state="Boolean(img)"
                          placeholder="Choose a image or drop it here..."
                          drop-placeholder="Drop image here..."
                        ></b-form-file>
                        <b-form-group
                          label="Description"
                          label-for="name-input"
                          invalid-feedback="Name is required"
                        >
                          <b-form-textarea
                            id="textarea"
                            v-model="formadd.note"
                            placeholder="Enter something..."
                            rows="6"
                            max-rows="8"
                          ></b-form-textarea>
                        </b-form-group>
                        <b-form-group label="Status">
                          <b-form-select
                            v-model="formadd.status"
                            :options="options"
                          ></b-form-select>
                        </b-form-group>
                      </b-col>
                      <b-col lg="3">
                        <b-form-group
                          label="Import price"
                          label-for="name-input"
                          invalid-feedback="Name is required"
                        >
                          <b-form-input
                            id="name-input"
                            v-model="formadd.import_price"
                            required
                          >
                          </b-form-input>
                        </b-form-group>
                        <b-form-group
                          label="Sale"
                          label-for="name-input"
                          invalid-feedback="Name is required"
                        >
                          <b-form-input
                            id="name-input"
                            v-model="formadd.sale"
                            required
                          >
                          </b-form-input>
                        </b-form-group>
                        <b-form-group
                          label="Export price"
                          label-for="name-input"
                          invalid-feedback="Name is required"
                        >
                          <b-form-input
                            id="name-input"
                            v-model="formadd.export_price"
                            required
                          >
                          </b-form-input>
                        </b-form-group>
                        <b-form-group label="Supplier">
                          <b-form-select
                            v-model="formadd.supplier_id"
                            :options="options"
                          ></b-form-select>
                        </b-form-group>
                      </b-col>

                      <b-col lg="3">
                        <div
                          style="display:flex,align-items: center;justify-content: center;"
                          v-for="(apartment, index) in apartments"
                          :key="`apartment - ${index}`"
                        >
                          <b-row>
                            <b-col lg="4">
                              <b-form-group label="Color">
                                <b-form-select
                                  v-model="formadd.color_id"
                                  :options="color"
                                  :name="`apartments[${index}][color_id]`"
                                ></b-form-select>
                              </b-form-group>
                            </b-col>
                            <b-col lg="4">
                              <b-form-group label="Size">
                                <b-form-select
                                  v-model="formadd.size_id1"
                                  :options="size"
                                  :name="`apartments[${index}][size_id]`"
                                ></b-form-select>
                              </b-form-group>
                            </b-col>
                            <b-col lg="4">
                              <b-form-group
                                label="Quantity"
                                label-for="name-input"
                                invalid-feedback="Name is required"
                               
                              >
                                <b-form-input
                                  id="name-input"
                                  type="number"
                           
                                   :name="`apartments[${index}][amount]`"
                                  required
                                >
                                </b-form-input>
                              </b-form-group>
                            </b-col>
                          </b-row>
                        </div>
                        <b-button variant="success" @click="addNewPartment()"
                      >Add</b-button
                    >
                      </b-col>
                    </b-row>
                    
                  </form>
                  
                </b-modal>

              </table>
            </template>
          </card>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Vue from "vue";
import axios from "axios";
import VueAxios from "vue-axios";
Vue.use(VueAxios, axios);
export default {
  data() {
    return {
      isEdit: null,
      status: 1,
      options: [
        { value: 1, text: "1" },
        { value: 0, text: "2" },
      ],
      supplier_id: 1,
      options: [
        { value: 1, text: "1" },
        { value: 0, text: "2" },
      ],
      Quantity:"11",
      products: [],
      formadd: {
          name: "",
        amount: "",
        img: "",
        note: "",
        price: "",
        sale: "",
        status: "",
        supplier_id: "",
        color_id:"",
        size_id:"",
        Quantity:""
      

      },
      formedit: {
        name: "",
        amount: "",
        img: "",
        note: "",
        price: "",
        sale: "",
        status: "",
        supplier_id: "",
        color_id:"",
        size_id:"",
        Quantity:""

      },

      apartments: [
        {
          color_id: "",
          size_id: "",
          amount: "1",
        },
      ],
      apartment: [
        {
          color_id: "",
          size_id: "",
          amount: "1",
        },
      ],
    };
  },
  props: {
    columns: Array,
    data: Array,
  },
  mounted() {},
  created() {
    this.getItem();
  },
  methods: {

    Count(){
      
    },
    addNewPartment() {
      this.apartments.push({
        color_id: "",
        size_id: "",
        amount: "",
      });
    },
    logOut() {
      var axa = "asda";
      console.log(axa);
    },
    addMoreData(index) {
      this.formadd.push({
        color_id: "",
        size_id: "",
        amount: "",
      });
    },
    getItem() {
      var self = this;
      Vue.axios
        .get("http://127.0.0.1:8000/api/product")
        .then(function (resp) {
          self.products = resp.data;
          console.log("Data:", resp.data.data);
        })
        .catch(function (error) {
          console.log("Loi:", error);
        });
    },
    addItem(payload) {
      const path = `http://127.0.0.1:8000/api/product`;
      axios
        .post(path, payload)
        .then(() => {
          this.getItem();
        })
        .catch((error) => {
          this.getItem();
          console.log(error);
        });
    },
    // edit(id) {
    //   this.isEdit = id;
    //   axios
    //     .get(`http://127.0.0.1:8000/api/product` + id)
    //     .then((res) => res.data)
    //     .then((response) => {
    //       const { data } = response;
    //       this.editform.name=data.name,
    //       this.editform.name=data.name,
    //       this.editform.name=data.name,
    //       this.editform.name=data.name,

    //     });
    // },
    update() {
      axios
        .put(
          `http://127.0.0.1:8000/material/detail_material/` + this.isEdit,
          this.editform,
          {}
        )
        .then((res) => {
          console.log(res.data);
          this.getMeterial();
          this.$refs.editSupModal.hide();
          this.$toaster.success("Sửa nguyên liệu thành");
        })
        .catch((err) => {
          this.$refs.editSupModal.hide();
          this.$toaster.error("Sửa nguyên liệu thất bại");
        });
    },
    handleOk() {
      // event.preventDefault();

      const payload = {
        name: this.formadd.name,
        status: this.formadd.status,

        date: this.formadd.date,
      };
      this.addItem(payload);
    },
    hasValue(item, column) {
      return item[column.toLowerCase()] !== "undefined";
    },
    itemValue(item, column) {
      return item[column.toLowerCase()];
    },
    checkFormValidity() {
      const valid = this.$refs.form.checkValidity();
      this.nameState = valid;
      return valid;
    },
    resetModal() {
      this.name = "";
      this.nameState = null;
    },
    handleOk(bvModalEvt) {
      // Prevent modal from closing
      bvModalEvt.preventDefault();
      // Trigger submit handler
      this.handleSubmit();
    },
    handleSubmit() {
      // Exit when the form isn't valid
      if (!this.checkFormValidity()) {
        return;
      }
      // Push the name to submitted names
      this.submittedNames.push(this.name);
      // Hide the modal manually
      this.$nextTick(() => {
        this.$bvModal.hide("add-product");
      });
    },
  },
};
</script>
<style>
.modal.show .modal-dialog {
  transform: translate(0, 50%);
  padding: 2px 0px;
}
.editcategory {
  border: none;
  padding: 4px 12px;
  margin-left: 1px;
  background-color: #0e6de9;
}
.editcategory:hover {
  color: #212529;
  background-color: #0e6de9;
}
.editcategory:active {
  color: #212529;
  background-color: #189ce9 !important;
}
.fixed {
  padding: 1px 1px;
}
/* .b-submit {
  background-color: red;
  color: black;
  padding: 1rem;
  cursor: pointer;
} */
</style>
