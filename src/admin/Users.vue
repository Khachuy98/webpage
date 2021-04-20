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
              <h4 class="card-title">Users list</h4>
              <p class="card-category">Here is a users</p>
              <div class="text-center">
                <button
                  type="submit" class="btn btn-info btn-fill float-right" 
                  v-b-modal.add-modal>Add new
                </button>
              </div>
                 <table class="table category">
                  <thead>
                    <slot name="columns">
                      <tr>
                        <th>ID</th>
                        <th>Name</th>
                        <th>Email</th>
                        <th>Created at</th>
                        <th>Action</th>
                      </tr>
                    </slot>
                  </thead>
                  <tbody>
                    <tr v-for="users in users.data" v-bind:key="users.id">
                      <td>{{ users.id }}</td>
                      <td>{{ users.name }}</td>
                      <td>{{ users.email }}</td>
                      <td> {{ users.created_at}}</td>
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
                    id="add-modal"
                    ref="modal"
                    title="Add users"
                    @show="resetModal"
                    @hidden="resetModal"
                    @ok="handleAdd"
                    cancel-title="Close"
                  >
                    <form @submit.prevent="SubmitAdd">
                      <b-form-group
                        label="Name"
                        label-for="name-input"
                        invalid-feedback="Name is required"
                      >
                        <b-form-input id="name-input" v-model="formadd.name" required>
                        </b-form-input>
                      </b-form-group>
                      <b-form-group
                        label="Email"
                        label-for="name-input"
                        invalid-feedback="Name is required"
                      >
                        <b-form-input id="name-input" type="email" v-model="formadd.email" required>
                        </b-form-input>
                      </b-form-group>
                      <b-form-group
                        label="Created At"
                        label-for="name-input"
                        invalid-feedback="Name is required"
                      >
                        <b-form-input id="name-input" type="date" v-model="formadd.created_at" required>
                        </b-form-input>
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
  name: "add-category",
  data() {
    return {
        dismissSecs: 3,
        dismissCountDown: 0,
        showDismissibleAlert: false,
      isEdit: false,
      users: [],
      formadd: {
        name: "",
        email: "",
        created_at: "",
      },
    };
  },
  name: "c-table",
  mounted() {},
  created() {
    this.getItem();
  },
  methods: {
    // logOut(){
    //   var axa = "asda";
    //   console.log(axa);
    // },
    getItem() {
      var self = this;
      Vue.axios
        .get("http://127.0.0.1:8000/api/users")
        .then(function(resp) {
          self.category1 = resp.data;
          console.log("Data:", resp.data.data);
        })
        .catch(function(error) {
          console.log("Loi:", error);
        });
    },

    addItem(payload) {
      const path = `http://127.0.0.1:8000/api/users`;
      axios
        .post(path, payload)
        .then(() => {
          this.getItem();
          console.log("Thành công");
        })
        .catch(error => {
          this.getItem();
          console.log("Lỗi", error);
        });
    },

    edit(id) {
      this.formedit.id = id;
      // var _this = this;
      console.log("http://127.0.0.1:8000/api/category/"+id);
      axios
        .get('http://127.0.0.1:8000/api/category/'+ id)
        .then(res=> {
          this.formedit.name = res.data.data.name;
          console.log(res.data.data.name);
          this.formedit.status = res.data.data.status;
          // console.log(_this.formedit.name ),
          // console.log(_this.formedit.status )
          console.log("Thành công");
        })
        .catch(function(error) {
          console.log("lỗi:", error);
        });
    },
    hasValue(item, column) {
      return item[column.toLowerCase()] !== "undefined";
    },
    itemValue(item, column) {
      return item[column.toLowerCase()];
    },
    checkFormValidity() {
      const valid = this.$refs.form.checkValidity();

      return valid;
    },
    resetModal() {
      this.name = "";
    },
    handleOk(bvModalEvt) {
      var _this = this;
      var isEdit = _this.formedit;
      console.log("http://127.0.0.1:8000/api/category/",isEdit);
      console.log("lay thu id",isEdit.id);
      axios
        .put('http://127.0.0.1:8000/api/category/'+isEdit.id,isEdit)
        .then((res) => {
          console.log(res.data.data);
          this.getItem();
          this.dismissCountDown = this.dismissSecs
        })
        .catch(function(error) {
          console.log("lỗi:", error);
           this.getItem();
        });
      // Prevent modal from closing
      bvModalEvt.preventDefault();
            this.$nextTick(() => {
        this.$bvModal.hide("modal-center");
      });
    },
 handleAdd(bvModalEvt) {
      var isAdd = this.formadd;
      axios
        .post(`http://127.0.0.1:8000/api/category`, isAdd)
        .then(res => {
          this.getItem();
          console.log("Thành công");
          this.dismissCountDown = this.dismissSecs;
        })
        .catch(error => {
          this.getItem();
          console.log("Lỗi", error);
        });
      bvModalEvt.preventDefault();
      this.$nextTick(() => {
        this.$bvModal.hide("add-modal");
      });
    }
  }
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
.b-submit {
  background-color: rgb(248, 23, 23);
  color: black;
  padding: 14px 10px;
  display: inline;
  cursor: pointer;
  border-radius: 5px;
}
.b-close {
  background-color: rgb(160, 160, 158);
  color: black;
  padding: 8px 9px;
  display: inline;
  cursor: pointer;
  border-radius: 5px;
}
</style>
