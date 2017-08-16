<template>
  <div>
    <button @click="visual=!visual">page1</button>
     <v-dialog :visual.sync="visual">
        <v-page2></v-page2> 
    </v-dialog>
  </div>
</template>

<script>
import VDialog from './Dialog.vue'
import VPage2 from './Page2.vue'
export default {
  name: 'v-page1',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      visual:false
    }
  },
  components:{
    VDialog,VPage2
  }
}
</script>

<style>
</style>
