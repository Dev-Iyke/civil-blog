<template>
  <div class="notes">
    <h1>Member Notes</h1>
    <div class="notes" v-for="note in ntes" :key="note.id">
      <!-- <h3>{{ note.title }}</h3> -->
      <SingleNote :nte="note"/>
    </div>
  </div>
</template>

<script>
import SingleNote from './SingleNote.vue'
export default {
  components: {SingleNote},
  props: ['ntes']

}
</script>

<style>

</style>