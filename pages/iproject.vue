<template>
  <div class="overflow-auto">
      <search v-on:search-text="searchText"/>
    <b-pagination
      v-model="currentPage"
      :total-rows="rows"
      :per-page="perPage"
      aria-controls="my-table"
    ></b-pagination>

    <p class="mt-3">Current Page: {{ currentPage }}</p>

    <b-table
      id="my-table"
      :items="urgentorders"
      :per-page="perPage"
      :current-page="currentPage"
      small
    ></b-table>
  </div>
</template>

<script>

import Search from '~/components/search.vue'
import axios from "axios"
  export default {
      components:{
          Search
      },
    data() {
      return {
        perPage: 3,
        currentPage: 1,
        urgentorders: []
      }
    },
    computed: {
      rows() {
        return this.urgentorders.length
      }
    },
    mounted() {
        this.getUrgentOrders()
    },
    methods: {
    
    async searchText(text){
    const config = {
       Header :{
         'Accept':'Application/json'
       }
     }
     try {
        
     const urgentorder = await axios.get(`http://localhost:8000/api/search/${text}`, config);
     this.$toast.success({
    title:'sucess',
    message:'You are done'
``  })
     this.urgentorders = urgentorder.data.data
     


     } catch (error) {
       console.log(error)
     }
    },
    async getUrgentOrders(){
    const config = {
      header :{
        'Accept':'Application/json'
      }
    }

    try {
      const urgentorder = await axios.get("http://localhost:8000/api/v1/urgency/all", config)
      
     
    
      this.urgentorders = urgentorder.data.data
     
   
    } catch (error) {
      console.log(error)
    }

  }
    },
  }
</script>