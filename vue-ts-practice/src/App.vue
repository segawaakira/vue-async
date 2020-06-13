<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <button @click="test()">てすとです</button>
    <pre>
      {{ arrayOne }}
    </pre>
    <pre>
      {{ arrayTwo }}
    </pre>
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
      arrayOne: [],
      arrayTwo: []
    }
  },
  methods: {
    async test() {
     try {
       const response1 = await axios.get('https://api.zipaddress.net/?zipcode=6028321');
       this.arrayOne = response1.data;
       const response2 = await axios.get(`https://api.zipaddress.net/?zipcode=1670` + response1.data.code);
       this.arrayTwo = response2.data;
     } catch(e) {
       console.log(e);
     }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
