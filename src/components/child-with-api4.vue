<template>
  <div>
    <h2>{{title}}</h2>
    <span>myObject.nestedObj.nestedNumberVal1 : </span>
    <br />
    <input v-model="myObject.nestedObj.nestedNumberVal1" type="number" />
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

  get title() {
      return 'child-with-api4.vue';
  }

  created() {
    console.log('created')
    this.$setPageDataCallback((data:any) => {
      console.log('child4.vue : $setPageDataCallback', data);
      // this.myObject = _.get(data, 'nestedObj.nestedStrVal1');
      this.myObject = data;
    },'pageObject');
  }
}
</script>
