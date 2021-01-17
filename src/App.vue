<template>
  <div id="app">
    <Header />
    <Chat />
  </div>
</template>

<script>
// @ is an alias to /src
import Header from "@/components/Header.vue";
import Chat from "@/components/Chat.vue";

export default {
  name: "App", 
  components: {
    Header,
    Chat
  } 
}
</script>

<style>
#app {
  margin: 0;
  padding: 0;
  font-family: 'Roboto', Helvetica, Arial, sans-serif;
  font-weight: 400;
  background-color: #ffffff;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
