<template>
  <div id="app">
    <button @click="visual=!visual">dialog</button>
     <v-dialog :visual.sync="visual" size="large">
        <v-page1></v-page1>
    </v-dialog>
  </div>
</template>

<script>
import VPage1 from './Page1.vue'
import VDialog from './Dialog.vue'
export default {
  name: 'app',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      visual:false
    }
  },
  components:{
    VDialog,
    VPage1
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 60px;
  width:100%;
  height:100%;
}
html,body{
  height:100%;
  width:100%;
}
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
