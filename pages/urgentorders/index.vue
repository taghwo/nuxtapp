<template>
  <section class="container">
  
    <div>
     <span>All Order Count:  {{orderscount}}</span>
     <span>All Refunds Count: {{refundscount}}</span>
     <span>All Complaints Count: {{complaintscount}}</span>
    </div>
    
    <search v-on:search-text="searchText"/>

  <h1 class="mt-2">Urgent Orders</h1>
  <table class="table-condensed table-striped shadow rounded table-hover  table-responsive">
    <tbody>
      <tr>
      <th>sn</th>
      <th>topic</th>
      <th>client number</th>
      <th>client email</th>
      <th>Date Of Delivery</th>
      <th>Delivery Type</th>
      <th>Action</th>
    </tr>
    <tr v-for="urgentorder in urgentorders" :key="urgentorder.id">
      <td>{{urgentorder.id}}</td>
      <td>{{urgentorder.topic}}</td>
      <td>{{urgentorder.client_phone_number}}</td>
      <td>{{urgentorder.client_email}}</td>
      <td>{{urgentorder.date_of_delivery}}</td>
      <td>{{urgentorder.time_of_delivery}}</td>
    
    </tr>
    </tbody>
    <tfoot>
    </tfoot>
    
  </table>
 

  <h1 class="mt-2">Urgent 48 hrs Orders</h1>
  <table class="table-condensed table-striped shadow rounded table-hover table-responsive">
    <tbody>
      <tr>
      <th>sn</th>
      <th>topic</th>
      <th>client number</th>
      <th>client email</th>
      <th>Date Of Delivery</th>
      <th>Delivery Type</th>
      <th>Action</th>
    </tr>
    <tr v-for="urgentfortyeighthoursorder in urgentfortyeighthoursorders" :key="urgentfortyeighthoursorder.id">
      <td>{{urgentfortyeighthoursorder.id}}</td>
      <td>{{urgentfortyeighthoursorder.topic}}</td>
      <td>{{urgentfortyeighthoursorder.client_phone_number}}</td>
      <td>{{urgentfortyeighthoursorder.client_email}}</td>
      <td>{{urgentfortyeighthoursorder.date_of_delivery}}</td>
      <td>{{urgentfortyeighthoursorder.time_of_delivery}}</td>
       <td><nuxt-link :to="'urgentorders/' + urgentfortyeighthoursorder.id">View More</nuxt-link></td>
    </tr>
    </tbody>
    <tfoot>
    </tfoot>
    
  </table>

   <h1 class="mt-2">Urgent 7 Days Orders</h1>
  <table class="table-striped table-hover  shadow rounded table-responsive">
    <tbody>
      <tr>
      <th>sn</th>
      <th>topic</th>
      <th>client number</th>
      <th>client email</th>
      <th>Date Of Delivery</th>
      <th>Delivery Type</th>
      <th>Action</th>
    </tr>
    <tr v-for="urgentsevendaysorder in urgentsevendaysorders" :key="urgentsevendaysorder.id">
      <td>{{urgentsevendaysorder.id}}</td>
      <td>{{urgentsevendaysorder.topic}}</td>
      <td>{{urgentsevendaysorder.client_phone_number}}</td>
      <td>{{urgentsevendaysorder.client_email}}</td>
      <td>{{urgentsevendaysorder.date_of_delivery}}</td>
      <td>{{urgentsevendaysorder.time_of_delivery}}</td>
       <td><nuxt-link :to="'urgentorders/' + urgentsevendaysorder.id">View More</nuxt-link></td>
    </tr>
    </tbody>
    <tfoot>
    </tfoot>
    
  </table>
  </section>
  </template>

<script>

import Logo from '~/components/Logo.vue'
import Search from '~/components/search.vue'
import axios from "axios"

export default {
  components: {
    Logo,
    Search,
   
  },
   
  head: {
        title: "Urgent orders",
        meta:[{
          hid:"description",
          name:"description",
          content:"All urgent orders"
        }]
  },
  data(){

    return {
      orderscount:'',
       refundscount:'',
        complaintscount:'',
        urgentorders:[],
        urgentfortyeighthoursorders: [],
        urgentsevendaysorders: [],
        resource_url: 'http://localhost:8000/api/v1/urgency/all'

    }

  },
 computed(){
   if(text.lenght > 1){
     this.searchText()
   }
 },
  mounted(){
     
    this.$nextTick(() => {
   this.$nuxt.$loading.start()
   setTimeout(() => this.$nuxt.$loading.finish(), 500)
    })
     console.log(this.text)
    this.getCounts()
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
     this.urgentorders = urgentorder.data.data

     } catch (error) {
       console.log(error)
     }
  },
  async getCounts() {
     const config = {
       Header :{
         'Accept':'Application/json'
       }
     }

     const auth = {
        bearer :{
         'Token':'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImQwZjZmNmJkNGUzNDk5NGZkMGJiY2JmODIzMWE2ZDBiNzFmNjljZDI1YzM1MjM3ZjI0NTQ4Yzc0ZTdmNjA2YWY2YTIyNTBlZjgxZDExNDlhIn0.eyJhdWQiOiIxIiwianRpIjoiZDBmNmY2YmQ0ZTM0OTk0ZmQwYmJjYmY4MjMxYTZkMGI3MWY2OWNkMjVjMzUyMzdmMjQ1NDhjNzRlN2Y2MDZhZjZhMjI1MGVmODFkMTE0OWEiLCJpYXQiOjE1NTgyMjc1NzksIm5iZiI6MTU1ODIyNzU3OSwiZXhwIjoxNTg5ODQ5OTc4LCJzdWIiOiI3MSIsInNjb3BlcyI6W119.sbUPc9RuhoMAEq06jfSKWWOTmTXjSqF7JNXyhXNw5uOYtPG7cFG8PEMkXINKiJlJyCMI6iJ06kIMAcPmN1yJacCJaw90A6PLw-dz5GgrCykAT-9Q84XMnGm0m3BbsnKUtggCv3gDfjGpp4ETWEwF6Jza7cUl8NUsmvI76f_Rmzf3WiC2qhMRKquGAoOkc5vWWrvTaV_OvQpt1rrLBgqeHKaFrm-K-n-DOcOoUzJt9eEf4gqzBQpuqg755r8_G-p-xplkz0ihGG5Z19E54PBg_j1ognX5ZIG8jKrIiwB3HJ0nUkkfiMJkhrVyBKNVswq_9QGds8JTNa949b-ktN3jhkG-9INpqzk0Px4phX00jz-V4bU2JEMy7m62tvn3cnv03OR7XUFwiFnDTTkTk-bSwTRBm2C9eGNjAu7CAGCG-h-E6InUzMM07CoUlETHZMkRDSNPMjtxYW4RKTY-VwIIoVwXdyH-q5U7zhGaTW8NlsNXrCW-5AuKDs06pXpL_xb3_aPgJG_e6iQUIUDEC6Nuvsy3M6JNuL5GgBypk19X8Xl0knjxVMEAuE5gRoKulrq2lW9dAkNZutvGrnbkWdBTc6NB8GlRD1LFfGW3I99VdxwwSNst7m_R7Qvu7kYcr9OzN7xAwUsA4-O2CLriNbMv5GcekkmI6hXPrV3hUIWfU_Q'
       }
     }

     try {
        
     const order = await axios.get("http://localhost:8000/api/v1/orders/count", config, auth);
     const refunds = await axios.get("http://localhost:8000/api/v1/refunds/count", config, auth);
     const complaint = await axios.get("http://localhost:8000/api/v1/complaints/count", config, auth);
     this.orderscount = order.data.data
     this.refundscount = refunds.data.data
     this.complaintscount = complaint.data.data

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
      
      const urgentorderfortyeighthoursorder = await axios.get("http://localhost:8000/api/v1/urgency/fortyeighthours", config)
    
     const urgentsevendays = await axios.get("http://localhost:8000/api/v1/urgency/sevendays", config)
    
      console.log(urgentorderfortyeighthoursorder.data)
    
      this.urgentorders = urgentorder.data.data
     
      this.urgentfortyeighthoursorders = urgentorderfortyeighthoursorder.data.data
    
      this.urgentsevendaysorders = urgentsevendays.data.data
      if(urgentsevendays.status != 'success')
      {
        this.$toast.success('saved').goAway(3000)
      }
        
    } catch (error) {
     
      console.log(error)
    }

  }
},
}
</script>

 <style scoped>

html{
   background: url('../../assets/svg/undraw_children_4rtb.svg');
   height:100%;
 
}
.container {
  margin: 0 auto;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;

  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
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
