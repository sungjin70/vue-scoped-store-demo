<template>
  <div>
    <h2>{{title}}</h2>

    <span>myObject.strValue1 : </span>
    <br />
    <input v-model="pageObject_strValue1" />
    <br />
    <span>myCounter : </span>
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
    'myObject.strValue1' : {
      deep: true,
      // eslint-disable-next-line @typescript-eslint/no-explicit-any
      handler (newVal : any, oldVal: any): void {
        this.$sendPageData(newVal,'pageObject.strValue1');
      }
    },
    myCounter : function (newVal : any, oldVal: any) {
      this.$sendPageData(newVal,'pageCounter');
    },
  },
})
export default class extends Vue {

  private myObject: any = null;
  // eslint-disable-next-line @typescript-eslint/no-inferrable-types
  private myCounter = -5;

  // eslint-disable-next-line @typescript-eslint/explicit-module-boundary-types
  get title() {
      return 'child-with-api1.vue';
  }

  get pageObject_strValue1() : string {
    try {
      return this.myObject.strValue1;
    } catch (error) {
      return "";
    }
  }

  set pageObject_strValue1(value:string) {
    this.myObject.strValue1 = value;
  }  

  created() {
    this.$setPageDataCallback((data:any) => {
      console.log('child1.vue : $setPageDataCallback', data);
      // this.myObject = _.get(data, 'nestedObj.nestedStrVal1');
      this.myObject = data;
    }, 'pageObject');

    this.$setPageDataCallback((data:any) => {
      console.log('child1.vue : $setPageDataCallback', data);
      this.myCounter = data;
    }, 'pageCounter');
  }

}
</script>
