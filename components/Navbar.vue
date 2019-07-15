<template>
    <ul :class="color " class="rounded shadow">
        <li><nuxt-link to="/">Thanos</nuxt-link></li>
        <li><nuxt-link to="/about">Vadar</nuxt-link></li>
        <li><nuxt-link to="/contact">Joker</nuxt-link></li>
         <li><nuxt-link to="/urgentorders">Bane</nuxt-link></li>
         <li><nuxt-link to="/iproject">Try</nuxt-link></li>
       
    </ul>
</template>

<script>
export default {
    
        name: "Navbar",
        props:['color'],

        data() {
            return {
                bg:this.color,
            }
        },
         mounted(){
             console.log(this.color)
         }
    
}
</script>


<style>
.black{
    background:skyblue;
    color:black
}
li a{
    color:white;
    text-decoration: none;
    text-decoration-line: none;
}
li a :hover{
    color:grey;
}
li{
   float: left;
   padding-right: 10px;
   text-decoration: none;
   list-style-type: none;
}
ul{
    display: flex;
}
</style>
