<template>
  <div class="note">
    <h3>{{ nte.title }}</h3>
    <p>{{ shortenNote }}</p>
  </div>
</template>

<script>
import { computed } from 'vue'
export default {
    props: ['nte'],

    setup(props){
        const shortenNote = computed(() => {
            return props.nte.body.substring(0, 110) + '...read more'
        })

        return {shortenNote}
    }



}
</script>

<style>

</style>