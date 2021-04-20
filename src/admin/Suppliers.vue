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
              <h4 class="card-title">Suppliers list</h4>
              <p class="card-category">Here is a suppliers</p>
              <div class="text-center">
                <button
                  type="submit" class="btn btn-info btn-fill float-right" 
                  v-b-modal.addmodal>Add new
                </button>
              </div>
                <table class="table supplier">
        <thead>
          <slot name="columns">
            <tr>
              <th>ID</th>
              <!-- <th>Category ID</th> -->
              <th>Name</th>
              <th>Address</th>
              <th>Phone</th>
              <th>Status</th>
              <th>Action</th>
            </tr>
          </slot>
        </thead>
        <tbody>
          <tr v-for="supplier in supplier.data" v-bind:key="supplier.id">
            <td>{{ supplier.id }}</td>
            <!-- <td>{{ supplier.category_id }}</td> -->
            <td>{{ supplier.name }}</td>
            <td>{{ supplier.address }}</td>
            <td> 0{{ supplier.phone }}</td>
            <td>{{ supplier.status }}</td>
            <td>
              <b-button
                class="btn editsupplier"
                variant="warning"
                v-b-modal.editmodal
                >Edit</b-button
              >
            </td>
          </tr>
        </tbody>
        <b-modal
          id="addmodal"
          ref="modal"
          title="Add Supplier"
          @show="resetModal"
          @hidden="resetModal"
        >
          <form ref="form" @submit.stop.prevent="handleSubmit">
            <b-form-group
              label="Name"
              label-for="name-input"
              invalid-feedback="Name is required"
            >
              <b-form-input id="name-input" v-model="addmodal.name" required> </b-form-input>
            </b-form-group>
            <b-form-group label="Category ID">
              <b-form-select v-model="addmodal.category_id" :options="options"></b-form-select>
            </b-form-group>
            <b-form-group
              label="Address"
              label-for="name-input"
              invalid-feedback="Name is required"
            >
              <b-form-input id="name-input" v-model="addmodal.address" required>
              </b-form-input>
            </b-form-group>
            <b-form-group
              label="Phone"
              label-for="name-input"
              invalid-feedback="Name is required"
            >
              <b-form-input type="text" id="name-input" v-model="addmodal.phone" required>
              </b-form-input>
            </b-form-group>
          </form>
        </b-modal>
        <b-modal
          id="editmodal"
          ref="modal"
          title="Edit Supplier"
          @show="resetModal"
          @hidden="resetModal"
        >
          <form ref="form" @submit.stop.prevent="handleSubmit">
            <b-form-group
              label="Name"
              label-for="name-input"
              invalid-feedback="Name is required"
            >
              <b-form-input id="name-input" v-model="editmodal.name" required> </b-form-input>
            </b-form-group>
            <b-form-group label="Category ID">
              <b-form-select v-model="editmodal.category_id" :options="options"></b-form-select>
            </b-form-group>
            <b-form-group
              label="Address"
              label-for="name-input"
              invalid-feedback="Name is required"
            >
              <b-form-input id="name-input" v-model="editmodal.address" required>
              </b-form-input>
            </b-form-group>
            <b-form-group
              label="Phone"
              label-for="name-input"
              invalid-feedback="Name is required"
            >
              <b-form-input type="text" id="name-input" v-model="editmodal.phone" required>
              </b-form-input>
            </b-form-group>
            <b-form-group label="Status">
              <b-form-select v-model="editmodal.status" :optionss="optionss"></b-form-select>
            </b-form-group>
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
          isEdit:null,
            supplier: [],
              addmodal :{
                name:"",
                category_id:"",
                address: "",
                phone: "",
                // status:"1",
                // date:"",
            },
            editmodal:{
                  name:"",
                  category_id:"",
                  address: "",
                  phone: "",
                  status:"1"
            },
            options: [
          { value: 1, text: 'Sneaker' },
          { value: 2, text: 'Boot' },
        ],
       optionss: [
          { value: 1, text: 'Active' },
          { value: 2, text: 'Inactive' },
        ]
    };
  },
  props: {
    columns: Array,
    data: Array,
  },
  mounted() {
    var self = this;
    Vue.axios
      .get("http://127.0.0.1:8000/api/supplier")
      .then(function (resp) {
        self.supplier = resp.data;
        console.log("Data:", resp.data.data);
      })
      .catch(function (error) {
        console.log("Loi:", error);
      });
  },
  methods: {
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
    },
  },
};
</script>
<style>
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
</style>
