<template>
<div>
    <select class="form-control" v-model="stateValue" @change="getLGA($event)">
        <option>Select State</option>
<option v-for="location in states" :key="location.state.id" :value="location.state.name">{{location.state.name}}</option>
    
                                       
    </select>

    <select class="form-control" v-model="lgaValue" @change="getLGAValue($event)">
        <option></option>
<option v-for="lga in lgas" :key="lga.id" :value="lga.name">{{lga.name}}</option>                                
    </select>
    <input type="search" name="searchusers" v-model="name" @keyup="getUser()" class="form-control">

    <div class="users" v-if="users">
        <div class="card" v-for="person in users" :key="person.id">
        <div class="card-header">
            {{person.name}}
        </div>
        <div class="card-body">
            {{person.email}}
        </div>
        <div class="card-footer">
             {{person.created_at}}
        </div>
    </div>
    </div>
    

</div>
</template>

<script>
import {ngstates} from '../allngstates'
import axios from "axios"
export default {

data(){
        return{
            name:'',
            lgaValue: '',
            stateValue: '',
            states: [],
            lgas:[],
            users:[]
        }
},
computed: {
    checkInput: function () {
        if(this.name.length == '0'){
            this.users = ''
        }
    }
    
},
mounted(){
    
    
    this.allStates();
    
    
},

methods:{
    getLGA(e){

        const seletedStateValue = e.target.value;

        //this.stateValue = seletedStateValue

        this.states.forEach((location) => {
        if(location.state.name == seletedStateValue){
            this.lgas = location.state.locals
        }
        })
    },
   async getLGAValue(e){
       try {
           
           const getQueryData = await this.querySearch();
            console.log(getQueryData)
       } catch (error) {
           console.log(error)
       }
        

        //this.lgaValue = e.target.value
    },

    async getUser() {
        try {

            if(this.name.length <= '0'){
            this.users = ''
        }else{
            
            const config = {
               headers: {
                    'accept':'application/json',
                    'Content-Type':'application/json'
               }
            }
            const keyword ={name:this.name};

            const users = await axios.post('http://localhost:3001/api/all-users',keyword,config);
            
             this.users = users.data;
             console.log(this.users)
        }
        } catch (error) {
            console.error(error)
        }
    },
    allStates() {
    this.states = ngstates;
        },
    querySearch()
    {
        return `${this.stateValue}  ${this.lgaValue}`
    }
        
    

}
}
</script>

<style>

</style>
