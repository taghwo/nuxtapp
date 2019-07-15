<template>
    <section class="container">
        <h1>We said no more surprises</h1>
        <p>But i was ready to pull off one last one</p>
    </section>
</template>

<script>
import pkg from '../package'
export default {

head() {
    return {
        title: 'About Page | '+ pkg.name,
        meta:[{
            hid:'description',
            name:'description',
            content: 'About iproject crm'
        }]
    }


}
}
</script>

<style scoped>
section{
    background: url('../assets/svg/undraw_children_4rtb.svg');
    background-position: center;
    background-attachment: fixed;
    background-size: contain;
    background-repeat: no-repeat;
    min-height: 100vh;
    font-family: cursive,Roboto;
}
</style>
