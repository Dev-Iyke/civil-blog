<template>
  <div class="members">
    <h2>Structural Members</h2>
    <input type="text" v-model="search">
    <p>Searched member: {{ search }}</p>
    <div v-for="m in matchedSearch" :key="m">
      <!-- <a href="/members">{{ m }}</a> -->
      {{ m }}
    </div>
    <button @click="stopWatching">Stop Watching</button>
  </div> <br>



  <div class="membersNotes">
    <p v-if="errorMessage">{{ errorMessage }}</p>
    <div v-if="notes.length">
      <MembersNotes :ntes="notes"/>
    </div>
    <div v-else>{{ searchStatus }}</div>
    
    
    
  </div>
</template>

<script>
import MembersNotes from '../components/MembersNotes'
import { computed, ref, watch, watchEffect } from 'vue';

export default {
    name: 'MembersView',
    components: { MembersNotes},
    setup(){

        //Structural Members Category
        const search = ref('')
        const members = ref(['slabs','beams','columns','cantilevers','props','joists','staircases'])

        const stopWatch = watch(search, () => {
          console.log('Do some stuff after every key we enter')
        })
        const stopEffect = watchEffect(() => {
          console.log('Do some stuff first once the components loads', search.value) 
        })
    
        const matchedSearch = computed(() => {
            return members.value.filter((mem) => mem.includes(search.value))
        })

        function stopWatching() {
          stopWatch()
          stopEffect()
        }


        //Notes Section
      /* const notes = ref([
        {title: 'Prestressed Concrete', code: '509', body: 'Lorem ipsum, dolor sit amet consectetur adipisicing elit. Quia qui quas voluptatum consequatur quisquam facilis cumque, recusandae quo? Possimus at adipisci totam quod molestiae incidunt odit aliquid consequuntur quos accusantium sunt rerum aperiam in molestias dolore labore natus magnam deleniti, laboriosam assumenda alias. Voluptatibus atque dicta molestiae architecto nisi vitae quod corporis et asperiores voluptates quia, ipsum, illo, eligendi rerum? Sequi, atque ratione. Voluptatum facilis vitae temporibus exercitationem placeat, excepturi natus, provident beatae, accusantium nam nisi! Necessitatibus accusantium magni deleniti, et culpa dolorem exercitationem quasi tenetur assumenda fugiat, beatae quas eos praesentium numquam facere, cum dolor distinctio perferendis cupiditate eveniet minus libero doloremque similique! Fugit ullam id mollitia expedita sint eveniet laborum eos facere. Assumenda nobis numquam eum possimus quo.'},
        {title: 'Reinforced Concrete', code: '518', body: 'Lorem ipsum, dolor sit amet consectetur adipisicing elit. Quia qui quas voluptatum consequatur quisquam facilis cumque, recusandae quo? Possimus at adipisci totam quod molestiae incidunt odit aliquid consequuntur quos accusantium sunt rerum aperiam in molestias dolore labore natus magnam deleniti, laboriosam assumenda alias. Voluptatibus atque dicta molestiae architecto nisi vitae quod corporis et asperiores voluptates quia, ipsum, illo, eligendi rerum? Sequi, atque ratione. Voluptatum facilis vitae temporibus exercitationem placeat, excepturi natus, provident beatae, accusantium nam nisi! Necessitatibus accusantium magni deleniti, et culpa dolorem exercitationem quasi tenetur assumenda fugiat, beatae quas eos praesentium numquam facere, cum dolor distinctio perferendis cupiditate eveniet minus libero doloremque similique! Fugit ullam id mollitia expedita sint eveniet laborum eos facere. Assumenda nobis numquam eum possimus quo.'},
        {title: 'Formwork For Concrete', code: '509', body: 'Lorem ipsum, dolor sit amet consectetur adipisicing elit. Quia qui quas voluptatum consequatur quisquam facilis cumque, recusandae quo? Possimus at adipisci totam quod molestiae incidunt odit aliquid consequuntur quos accusantium sunt rerum aperiam in molestias dolore labore natus magnam deleniti, laboriosam assumenda alias. Voluptatibus atque dicta molestiae architecto nisi vitae quod corporis et asperiores voluptates quia, ipsum, illo, eligendi rerum? Sequi, atque ratione. Voluptatum facilis vitae temporibus exercitationem placeat, excepturi natus, provident beatae, accusantium nam nisi! Necessitatibus accusantium magni deleniti, et culpa dolorem exercitationem quasi tenetur assumenda fugiat, beatae quas eos praesentium numquam facere, cum dolor distinctio perferendis cupiditate eveniet minus libero doloremque similique! Fugit ullam id mollitia expedita sint eveniet laborum eos facere. Assumenda nobis numquam eum possimus quo.'}
      ]) */
      const notes = ref([])
      const errorMessage = ref(null)
      const searchStatus = ref('Searching for data...')
      
      const runFunc = setTimeout(() =>{
        courseData()
      }, 2000)
      

      const courseData = async () => {
        try {
          let dataNotes = await fetch('http://localhost:3000/notes')
          console.log(dataNotes)
          if(!dataNotes.ok){
            throw Error('Data not found')
          }
          notes.value = await dataNotes.json()
          
        } catch (error) {
          errorMessage.value = error.message
          searchStatus.value = null;
          

        }
      }
      /* courseData() */

        return {
            members, search, matchedSearch, stopWatching, notes, errorMessage, searchStatus
        }
      

      
    }

    /* setUp(name){
      console.log(name)
    } */

}
</script>

<style>

</style>