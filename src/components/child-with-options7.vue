<template>
  <div>
    <h2>{{title}}</h2>
    <span>nestedStrVal1 (path:pageObject.nestedObj.nestedStrVal1) : </span>
    <br />
    <input v-model="nestedStrVal1" />
  </div>
</template>

<script lang='ts'>
import Vue from 'vue';
import Component from 'vue-class-component';
import _ from 'lodash';

@Component({
  pageStore:{
    nestedStrVal1:{
      //direction:'both', //read / write / both  - default:both
      path:'pageObject.nestedObj.nestedStrVal1', // a path of store. default:the same as key
      //deep:true, //an option of watch
      //immediate:true, //an option of watch
      // onBeforeSend: function(val:any, oldVal:any, options:{proceed:boolean}) {
      //   console.log('onBeforeSend for pageObject.nestedObj.nestedStrVal1 in child-with-options3', val, oldVal, options);
      // },
      // onBeforeReceive: function(val:any, oldVal:any, options:{proceed:boolean}) {
      //   console.log('onBeforeReceive for pageObject.nestedObj.nestedStrVal1 in child-with-options3', val, oldVal, options);
      // },
    },
  },
})
export default class extends Vue {

  private nestedStrVal1 = "nestedStrVal1 default";

  get title():string {
      return 'child-with-options7.vue';
  }
}
</script>
