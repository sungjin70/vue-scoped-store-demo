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
import _ from 'lodash';

@Component({
  pageStore:{
    nestedStrVal1:{
      //direction:'both', //read / write / both  - default:both
      path:'pageObject.nestedObj.nestedNumberVal1', // a path of store. default:the same as key
      //deep:true, //an option of watch
      //immediate:true, //an option of watch
      // onBeforeSend: function(val:any, oldVal:any, options:{proceed:boolean}) {
      //   console.log('onBeforeSend for pageObject.nestedObj.nestedNumberVal1 in child-with-options4', val, oldVal, options);
      // },
      // onBeforeReceive: function(val:any, oldVal:any, options:{proceed:boolean}) {
      //   console.log('onBeforeReceive for pageObject.nestedObj.nestedNumberVal1 in child-with-options4', val, oldVal, options);
      // },
    },
  },
  // watch: {
  //   'myObject.nestedObj.nestedNumberVal1' : function (newVal : any, oldVal: any) {
  //     this.$sendPageData(newVal,'nestedObj.nestedNumberVal1');
  //   },
  // },
})
export default class extends Vue {

  private nestedStrVal1 = -100;

  get title() : string {
      return 'child-with-options4.vue';
  }
}
</script>
