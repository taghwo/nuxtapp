<template>
    <div>
        <nuxt-link to="/urgentorders">Back to all urgent orders</nuxt-link>
        <h1>Order details</h1>
    
        <div class="card">
            <div class="card-header">
                <p>Topic: {{order.topic}}</p>
            </div>
            <div class="card-body">
                <p>Client Phone: {{order.client_phone_number}}</p>
                <hr>
                <p>Client Email: {{order.client_email}}</p>
                <hr>
                <p>Delivery Date: {{order.date_of_delivery}}</p>
                <hr>
                <p>Time Of Delivery: {{order.time_of_delivery}}</p>
                <hr>
                <p>Delivery Status: {{order.status == 0 ? 'Pending' : 'delivered'}}</p>
                <hr>
                  
            </div>
            <div class="card-footer">
                <small>This order was lodged by {{order_staff.staff_name}} on {{order.created_at}}</small>
            </div>
        <p>{{$route.params.id}}</p>
    </div>
    </div>
</template>

<script>
import pkg from '../../package'
import axios from "axios"
export default {


  data(){

    return {
       id: '',
       topic:'',
       client_phone_number:'',
       client_email:'',
       date_of_delivery:'',
       time_of_delivery:'',
       status:'',
       staff_name:'',
       created_at:'',
       order:[],
       order_staff:[]

    }

  },

  mounted(){
    this.getUrgentOrdersDetails(() => {
   this.$nuxt.$loading.start()
   setTimeout(() => this.$nuxt.$loading.finish(), 500)
    })
  },
  methods:{
async getUrgentOrdersDetails() {
    const config = {
        headers : {
            "Accept":"Application/json"
        }
    }
    const data = {
        id:this.$route.params.id
    }
    try {
         
        const order = await axios.post("http://localhost:8000/api/v1/orders/single",data,config)
        console.log(order)
        this.order = order.data.data
        this.order_staff = order.data.data.staff
    } catch (error) {
        console.log(error)
    }
  }
  
},
 head(){
     return{
          title: this.topic +" | " +pkg.name,
        meta:[{
          hid:"description",
          name:"description",
          content:this.topic +" | " +pkg.name
        }]
  
     }
       

},
}
</script>

<style>

</style>
