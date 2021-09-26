<template>
  <div>
    <h2>{{title}}</h2>
    <span>nestedStrVal1 (path:pageObject.nestedObj.nestedStrVal1): </span>
    <br />
    <input v-model="nestedStrVal1" />
  </div>
</template>

<script lang='ts'>
import Vue from 'vue';
import Component from 'vue-class-component';
import _ from 'lodash';

@Component({
  watch: {
    nestedStrVal1 : function (newVal : string, oldVal: string) {
      if (newVal !== oldVal)
        this.$sendPageData(newVal,'pageObject.nestedObj.nestedStrVal1');
    },
  },
})
export default class extends Vue {

  private nestedStrVal1 = 'nestedStr default';

  get title() {
      return 'child-with-api3.vue';
  }

  created() {
    this.$setPageDataCallback((data:any) => {
      this.nestedStrVal1 = data;
    }, 'pageObject.nestedObj.nestedStrVal1');
  }

}
</script>
