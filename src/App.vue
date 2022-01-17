<template>
  <div id="app">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <ul>
      <li v-for='item in list' :key='item.id'>
        {{item.name}}
      </li>
    </ul>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import axios from 'axios'
export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data() {
    return {
      list: []
    }
  },
  mounted(){
   axios.get('http://localhost:3000/api/users').then(res=>{
      console.log(res.data)
       this.list = res.data
   })
  }

}
</script>

<style>

</style>
