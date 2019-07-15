<template>
  <section class="container">
    
    <h1 class="justify-center" style="margin-top:20%">No amount of money ever bought a second of time</h1>
    <h2 class="mt-3">{{ title }}</h2>
    <div class="left">
    <ul>
      <li v-for="(link, index) in links" :key="index">
          {{link}}
      </li>
      
    </ul>
    </div>
    <div class="right">
      <!-- <stats /> -->
    </div>
  </section>
  
 
  </template>

<script>
import Stats from '../components/Stats';
import {mapState} from 'vuex';
import pkg from '../package';
import meta from '../meta';
export default {
  components: {
    stats
  },
  computed: {
    ...mapState([
    'title',
    'links'
  ])
  }, 
  head: {
        title: meta.home.title +" | "+ pkg.name,
        meta:[{
          hid:"description",
          name:"description",
          content:meta.home.description,
          charset:meta.home.charset
        }]
  }
  
}
</script>

 <style scoped>
section{
    background: url('../assets/svg/undraw_young_and_happy_hfpe.svg');
     background-position: center;
    background-attachment: fixed;
    background-size: contain;
    background-repeat: no-repeat;
    min-height: 100vh;
    font-family: cursive,Roboto;
}

.container {
  margin: 0 auto;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding-bottom:50px;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;

  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
  padding-top: 70px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
