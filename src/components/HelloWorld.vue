<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      
    </p>
    <h2>This is a API demo application for ScopedStore</h2>
    <h4>Examples in this API demo show you many things you can do with ScopedStore</h4>

  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class HelloWorld extends Vue {
  @Prop() private msg!: string;
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
