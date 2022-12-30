<template>
   <div>
      <Navbar />
      <div class="container" style="margin-top:4rem;">
        <h2>List Menu</h2>
      </div>
   </div>
</template>


<script>
// @ is an alias to /src
import Navbar from '@/components/NavbarComponent.vue'

export default {
  name: 'MenuView',
  components: {
    Navbar
  }
}
</script>
