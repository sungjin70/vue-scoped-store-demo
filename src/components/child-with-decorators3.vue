<template>
  <div>
    <h2>{{title}}</h2>
    <span>nestedStrVal1 (pageObject.nestedObj.nestedStrVal1) : </span>
    <br />
    <input v-model="nestedStrVal1" />
  </div>
</template>

<script lang='ts'>
import Vue from 'vue';
import Component from 'vue-class-component';
import {PageStore} from 'vue-scoped-store';

@Component
export default class extends Vue {

  @PageStore({path:"pageObject.nestedObj.nestedStrVal1"})
  private nestedStrVal1 = "nestedStrVal1 default";

  get title(): string {
      return 'child-with-decorators3.vue';
  }

}
</script>
