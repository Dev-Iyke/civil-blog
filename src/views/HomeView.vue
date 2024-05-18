<template>
  <h1>Civil Engineering Blog</h1>
  <h3 ref="top">Topic: {{ civTopic }}, with a rating of {{ civRating }}</h3>
  <input type="text" v-model="civTopic">
  <button @click="next">Next Topic</button><br>
  <button @click="civRating--">Reduce Rating</button>
</template>

<script>
import { ref } from 'vue';

export default {
  name: 'HomeView',
  setup(){
    const topic = ref('Flat Slabs')
    const rating = ref(8);

    const top = ref('null')
    console.log(top, top.value)
   

    const next = () =>{
      console.log(topic);
      console.log(top, top.value)

      top.value.classList.add('navy')
      topic.value = 'Waffle Slabs'
      rating.value = 6

      console.log(topic)
      console.log(rating)      
    }


    return {
      civTopic:topic, civRating: rating, next:next, top:top,
    }
    
  }
}
</script>

<style>
  .navy{
    background-color: navy;
    color: gold;
    padding: 10px;
  }
</style>
