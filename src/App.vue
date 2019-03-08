<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld v-bind:msg="msg"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
const ws = new WebSocket("ws://media.local:9229");

export default {
  name: 'app',
  components: {
    HelloWorld
  },
  data: function() {
    return {
      msg: ""
    }
  },
  methods: {
    setMessage: function(msg) {
      const payload = JSON.parse(msg.data);
      this.msg = `User ${payload.name} signed up using email ${payload.email}`;
    }
  },
  created: function() {
    ws.addEventListener('message', this.setMessage);
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
  margin-top: 60px;
}
</style>
