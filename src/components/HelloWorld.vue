<template>
  <div class="hello">
    <h5 position="relative">{{ msg }}</h5>
    <h6 margin="0" padding="0">Or just a normal stopwatch.</h6>
    <p><span></span></p>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'

@Component
export default class HelloWorld extends Vue {
  @Prop() private msg!: string;
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
p span {
  display: block;
}
</style>
