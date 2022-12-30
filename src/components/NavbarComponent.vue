<template>
  <div>
    <b-navbar toggleable="lg" variant="faded" type="orange">
      <div class="container">
        <b-navbar-brand href="#">Donut's Vue</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <router-link class="nav-link" to="/">Home</router-link>
            <router-link class="nav-link" to="/menus">Menu</router-link>
            <!-- <b-nav-item href="#">Link</b-nav-item> -->
          </b-navbar-nav>

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <b-nav-form>
              <b-form-input
                size="sm"
                class="mr-sm-2"
                placeholder="Search"
              ></b-form-input>
              <b-button size="sm" class="my-2 my-sm-0" type="submit"
                >Search</b-button
              >
            </b-nav-form> 

            <b-nav-item-dropdown right>
              <!-- Using 'button-content' slot -->
              <template #button-content>
                <em>User</em>
              </template>
              <b-dropdown-item href="#">Profile</b-dropdown-item>
              <b-dropdown-item href="#">Sign Out</b-dropdown-item>
            </b-nav-item-dropdown>

            <b-navbar-nav>
                <router-link class="nav-link" to="/">
                    <b-icon-bag class="mr-1"></b-icon-bag>
                    <span class="badge badge-chocolate my-auto">2</span>
                </router-link>  
            </b-navbar-nav>

          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: "NavbarComponent",
};
</script>
 