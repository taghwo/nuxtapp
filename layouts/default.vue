<template>
  <div class="container">
    <Navbar color="black"/>
    <nuxt />
   
  </div>
</template>

<script>
import Navbar from '~/components/Navbar.vue'
export default {
  components: {
    Navbar
  }
}
</script>

<style>
*{
  margin: 0;
  padding:5px;

}
html{
  
   background-position: center;
   background-repeat: no-repeat;

}
</style>
