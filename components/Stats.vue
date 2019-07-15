<template>
<div>
    <h2>Links count</h2>
    <p>{{ countLinks }}</p>
</div>
</template>

<script>
import {mapGetters} from 'vuex';
export default {
name : 'Stats',
computed: {
    ...mapGetters([
        'countLinks'
    ]),
}

}
</script>

<style>

</style>
