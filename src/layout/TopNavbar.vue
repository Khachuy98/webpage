<template>
  <nav class="navbar navbar-expand-lg">
    <div class="container-fluid">
      <div class="collapse navbar-collapse justify-content-end">
        <ul class="nav navbar-nav mr-auto">
          <b-nav-form>
            <b-form-input class="mr-sm-2" placeholder="Search"></b-form-input>
            <b-button variant="outline-success" class="my-2 my-sm-search" type="submit">Search</b-button>
          </b-nav-form>
        </ul>
        <ul class="navbar-nav ml-auto">
          <li class="nav-item">
            <b-dropdown text="Account">
              <b-dropdown-item href="#">Setting</b-dropdown-item>
              <b-dropdown-item href="#">Change Password</b-dropdown-item>
            </b-dropdown>
          </li>
          <li class="nav-item">
            <a href="#"  class="nav-link">
              Log out
            </a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>
<script>
  export default {
    computed: {
      filtersearch:function(){

      },
      routeName () {
        const {zet} = this.$route
        return this.capitalizeFirstLetter(zet)
      }
    },
    data () {
      return {
        search:'',
        activeNotifications: false
      }
    },
   created() {

    },
    methods: {
      capitalizeFirstLetter (string) {
        return string.charAt(0).toUpperCase() + string.slice(1)
      },
      toggleNotificationDropDown () {
        this.activeNotifications = !this.activeNotifications
      },
      closeDropDown () {
        this.activeNotifications = false
      },
      toggleSidebar () {
        this.$sidebar.displaySidebar(!this.$sidebar.showSidebar)
      },
      hideSidebar () {
        this.$sidebar.displaySidebar(false)
      }
    }
  }

</script>
<style>
  .mr-sm-2{
    border-radius: 12px;
  }
  .my-2 my-sm-search{
    border-radius: 12px;
  }
</style>
