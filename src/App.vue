<script setup>
// import { RouterLink, RouterView } from 'vue-router'
import { RouterView } from 'vue-router'
// import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <!-- <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    
    <div class="wrapper">
      
      <div>{{ greetings }}</div>


      <HelloWorld msg="You did it!" />

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
        <RouterLink to="/contact">Contact</RouterLink>
      </nav>
    </div>
  </header> -->

  <RouterView />
</template>

<script>
import {ref} from 'vue'

export default {
  setup() {
    const greetings = ref("Hello")
    return {
      greetings
    }
  },
}
</script>


<style scoped>

</style>
