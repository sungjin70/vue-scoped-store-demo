<template>
  <div>
    <h2>{{title}}</h2>
    
    <span>numberValue1 (path:pageObject.numberValue1) : </span>
    <br />
    <input v-model="numberValue1" type="number" />
  </div>
</template>

<script lang='ts'>
import Vue from 'vue';
import Component from 'vue-class-component';
import _ from 'lodash';

@Component({
  watch: {
    numberValue1 : function (newVal : any, oldVal: any) {
      this.$sendPageData(newVal,'pageObject.numberValue1');
    },
  },
})
export default class extends Vue {

  private numberValue1 = 0;

  get title() {
      return 'child-with-api2.vue';
  }

  created() {
    // _.set(this.myObject,'numberValue2', 0);
    this.$setPageDataCallback((data:any) => {
      this.numberValue1 = data;
      // this.myObject = data;
    }, 'pageObject.numberValue1');
  }

}
</script>
