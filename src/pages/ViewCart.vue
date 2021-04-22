<template>
  <div class="viewcart-1">
    <h2>View Cart</h2>
    <b-container class="content">
          <b-table
            sticky-header
            class="table-ct"
            striped
            hover
            :items="items"
            :fields="fields"
            head-variant="dark"
          >
          <template v-slot:cell(actions)="data">
            <b-button variant="primary" size="sm" class="mr-2" @click="payment(data.id)">Payment</b-button>
            <b-button variant="danger" size="sm" @click="delete(data.id)">Remove</b-button>
          </template>
          </b-table>
          <b-button variant="primary">Payment</b-button>
    </b-container>
    <top-nav-home />
    <content-footer-home />
  </div>
</template>

<script>
import ContentFooterHome from "../components/Footer/ContentFooterHome.vue";
import TopNavHome from "../layout/TopNavHome.vue";
export default {
  components: { ContentFooterHome, TopNavHome },
  data() {
    return {
      fields:[
        {
         key: 'name',
         label: 'Name'
        },
        {
         key: 'email',
         label: 'Email'
        },
        {
         key: 'age',
         label: 'Age',
         sortable: true
        },
        {
         key: 'actions',
         label: 'Actions',
        },
    ],
      items: [
        {
          id: 1,
          name: "Huy",
          email: "shyneward123@gmail.com",
          age: "23"
        },
        {
          id: 2,
          name: "Vũ",
          email: "shyneward123@gmail.com",
          age: "19"
        },
                {
          id: 2,
          name: "Vũ",
          email: "shyneward123@gmail.com",
          age: "19"
        },
                {
          id: 2,
          name: "Vũ",
          email: "shyneward123@gmail.com",
          age: "19"
        },
                {
          id: 2,
          name: "Vũ",
          email: "shyneward123@gmail.com",
          age: "19"
        },
                {
          id: 2,
          name: "Vũ",
          email: "shyneward123@gmail.com",
          age: "19"
        },
      ],
    };
  },
};
</script>

<style scoped>
.viewcart-1 {
  margin-top: 80px;
}
h2 {
  font-weight: bolder;
  text-transform: uppercase;
  text-align: center;
  margin-top: 130px;
}
.content {
  margin-bottom: 30px;
}
.table-ct {
  color: black;
}
</style>