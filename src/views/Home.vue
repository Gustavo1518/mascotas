<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logoDog.jpg">
    <HelloWorld msg="Welcome to mascotas"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  }
}
</script>
