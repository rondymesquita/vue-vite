<script>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
// import HelloWorld from './components/HelloWorld.vue'
import { ref, computed, defineAsyncComponent } from 'vue'
// import HelloWorld from "../docs/README.md";
const modules = import.meta.glob("../docs/*.md");

// console.log('aqui', modules);
export default {
  setup() {

    const components = computed(() => {

      // const comp = import("../docs/README.md")
      // defineAsyncComponent(() => comp)

      const modules = import.meta.glob("../docs/*.md");
      return Object.entries(modules).map(([path, definition]) => {
        console.log(definition);
        return defineAsyncComponent(definition)
      })
    })

    return {
      components
    }

  },
};

</script>

<template>

  {{counter}}

  <div v-for='(item, index) in components' :key='index' >
    <component :is='item'></component>
  </div>
</template>

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
