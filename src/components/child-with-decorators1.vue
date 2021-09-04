<template>
  <div>
    <h2>{{title}}</h2>
    <span>myCounter (path:pageCounter) : </span>
    <br />
    <input v-model="myCounter" type="number" />
    <br />
    <span>myObject.strValue1 : </span>
    <br />
    <input v-model="myObject.strValue1" />
    <br />
    <input v-model="myObject.strValue2" />
    <br />
    <span>pageObject:{{myObject}}</span>
  </div>
</template>

<script lang='ts'>
import Vue from 'vue';
import Component from 'vue-class-component';
import {PageStore} from 'vue-scoped-store';

@Component({})
export default class extends Vue {

  @PageStore({path:'pageObject',deep:true})
  private myObject = {strValue1:"8888",strValue2:"44444"};

  @PageStore({path:'pageCounter'})
  private myCounter = 5;

  get title() : string {
      return 'child-with-decorators1.vue';
  }

}
</script>
