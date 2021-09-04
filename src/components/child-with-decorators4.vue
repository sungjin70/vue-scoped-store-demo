<template>
  <div>
    <h2>{{title}}</h2>
    <span>myObject.nestedObj.nestedNumberVal1 : </span>
    <br />
    <input v-model="nestedStrVal1" type="number" />
  </div>
</template>

<script lang='ts'>
import Vue from 'vue';
import Component from 'vue-class-component';
import {PageStore} from 'vue-scoped-store';

@Component
export default class extends Vue {

  @PageStore({path:'pageObject.nestedObj.nestedNumberVal1'})
  private nestedStrVal1 = -100;

  get title():string {
      return 'child-with-decorators4.vue';
  }
}
</script>
