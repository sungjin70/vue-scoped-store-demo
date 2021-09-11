<template>
  <div>
    <h2>{{title}}</h2>
    <span>myObject.nestedObj.nestedNumberVal1 : </span>
    <br />
    <input v-model="myObject_nestedObj_nestedNumberVal1" type="number" />
  </div>
</template>

<script lang='ts'>
import Vue from 'vue';
import Component from 'vue-class-component';
import _ from 'lodash';

@Component({
  watch: {
    'myObject.nestedObj.nestedNumberVal1' : function (newVal : any, oldVal: any) {
      this.$sendPageData(newVal,'pageObject.nestedObj.nestedNumberVal1');
    },
  },
})
export default class extends Vue {

  private myObject: any = null

  get title(): string {
      return 'child-with-api4.vue';
  }

  get myObject_nestedObj_nestedNumberVal1(): string {
    try {
      return this.myObject.nestedObj.nestedNumberVal1;
    } catch (error) {
      return "";
    }
  }

  set myObject_nestedObj_nestedNumberVal1(value:string) {
    this.myObject.nestedObj.nestedNumberVal1 = value;
  }  

  created(): void {
    console.log('created')
    this.$setPageDataCallback((data:any) => {
      console.log('child4.vue : $setPageDataCallback', data);
      // this.myObject = _.get(data, 'nestedObj.nestedStrVal1');
      this.myObject = data;
    },'pageObject');
  }
}
</script>
