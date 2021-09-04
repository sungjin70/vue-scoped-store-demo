<template>
  <div>
    <h2>{{title}}</h2>
    <span>myNumber (pageObject.numberValue1) : </span>
    <br />
    <input v-model="myNumber" type="number" />
  </div>
</template>

<script lang='ts'>
import Vue from 'vue';
import Component from 'vue-class-component';
import {PageStore} from 'vue-scoped-store';

@Component
export default class extends Vue {

  @PageStore({path:"pageObject.numberValue1"})
  private myNumber = -100;
  
  get title():string {
      return 'child-with-decorators2.vue';
  }
}
</script>
