<template>
  <div>
    <h2>{{title}}</h2>

    <span>strValue1 (path:pageObject.strValue1) : </span>
    <br />
    <input v-model="strValue1" />
    <br />
    <span>myCounter (path:myCounter): </span>
    <br />
    <input v-model="myCounter" type="number" />
  </div>
</template>

<script lang='ts'>
import Vue from 'vue';
import Component from 'vue-class-component';
// import _ from 'lodash';

@Component({
  watch: {
    strValue1 : {
      // eslint-disable-next-line @typescript-eslint/no-explicit-any
      handler (newVal : any, oldVal: any): void {
        if (newVal != oldVal) 
        {
          this.$sendPageData(newVal,'pageObject.strValue1');
        }
      }
    },
    myCounter : function (newVal : any, oldVal: any) {
      if (newVal != oldVal) 
      {
        console.log('myCounter => sending data');
        this.$sendPageData(newVal,'pageCounter');
      }
    },
  },
})
export default class extends Vue {

  private strValue1 = '';
  // eslint-disable-next-line @typescript-eslint/no-inferrable-types
  private myCounter = -5;

  // eslint-disable-next-line @typescript-eslint/explicit-module-boundary-types
  get title() {
      return 'child-with-api1.vue';
  }

  created() {
    this.$setPageDataCallback((data:any) => {
      console.log('child1.vue : $setPageDataCallback', data);
      // this.myObject = _.get(data, 'nestedObj.nestedStrVal1');
      this.strValue1 = data;
    }, 'pageObject.strValue1');

    this.$setPageDataCallback((data:any) => {
      console.log('child1.vue : $setPageDataCallback', data);
      this.myCounter = data;
    }, 'pageCounter');
  }

}
</script>
