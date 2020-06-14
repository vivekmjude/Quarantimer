<template>
  <div class="home">
    <img alt="Vue logo" width="40%" height="25%" src="../assets/logo.png">
    <HelloWorld msg="A Timer, for your time in quarantine."/>
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
