<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld
  },
  mounted(){
    this.test()
  },
  methods:{
    test(){
      return ()=>{
        console.log(`我是es5`);
      }
    }
  }
};
</script>

<style lang="less">
:fullscreen {
  color:red
}
body {
  color: lch(53 105 40);
}
</style>
