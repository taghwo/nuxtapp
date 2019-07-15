<template>
    <form>
        <input type="search" v-model="text" @keydown="onSubmit" class="form-control">
        <!--input type="submit" value="submit" class="btn btn-sm btn-primary"-->
    </form>
</template>

<script>
export default {
name:"search",
data() {
    return {
         text:''
    }
   
}, 

methods :{
    onSubmit() {
        this.$emit("search-text",this.text)
      
    }
},
}
</script>

<style>

</style>
