<template>
  <div>
    <h2>Using typed-store with API</h2>
    <table width='100%' >
      <tr>
        <td>
          <p align="left">
            <b>pageObject : {</b>
            <br />
            <b>&nbsp;&nbsp;strValue1 : </b><input v-model="pageObject.strValue1" style="width:300px" /> ,
            <br />
            <b>&nbsp;&nbsp;strValue2 : </b><input v-model="pageObject.strValue2" style="width:300px" /> ,
            <br />
            <b>&nbsp;&nbsp;numberValue1 : </b><input v-model="pageObject.numberValue1" type="number" /> ,
            <br />
            <b>&nbsp;&nbsp;nestedObj : {</b>
            <br />
            <b>&nbsp;&nbsp;&nbsp;&nbsp;nestedStrVal1 : </b><input v-model="pageObject.nestedObj.nestedStrVal1" style="width:300px" /> ,
            <br />
            <b>&nbsp;&nbsp;&nbsp;&nbsp;nestedNumberVal1 : </b><input v-model="pageObject.nestedObj.nestedNumberVal1" type="number" /> ,
            <br />
            <b>&nbsp;&nbsp;}</b>
            <br />
            <b>}</b>
          </p>

          <button @click="updatePageObject()">updatePageObject()</button>
        </td>
        <td>
          <p align="left">
            <b>globalObject : {</b>
            <br />
            <b>&nbsp;&nbsp;strValue1 : </b><input v-model="globalObject.strValue1" style="width:300px" /> ,
            <br />
            <b>&nbsp;&nbsp;numberValue1 : </b><input v-model="globalObject.numberValue1" type="number" /> ,
            <br />
            <b>&nbsp;&nbsp;nestedObj : {</b>
            <br />
            <b>&nbsp;&nbsp;&nbsp;&nbsp;nestedStrVal1 : </b><input v-model="globalObject.nestedObj.nestedStrVal1" style="width:300px" /> ,
            <br />
            <b>&nbsp;&nbsp;&nbsp;&nbsp;nestedNumberVal1 : </b><input v-model="globalObject.nestedObj.nestedNumberVal1" type="number" /> ,
            <br />
            <b>&nbsp;&nbsp;}</b>
            <br />
            <b>}</b>
          </p>

        </td>
      </tr>
      <tr>
        <td>
          <p>
            <b>pageCounter : </b><input v-model="pageCounter" type="number" /> 
          </p>
          <button @click="pageCounter = Number(pageCounter) + 10">pageCounter + 10</button>
        </td>
        <td>
          <p>
            <b>globalCounter : </b><input v-model="globalCounter" type="number" /> 
          </p>
          <button @click="globalCounter = Number(globalCounter) + 10">globalCounter + 10</button>
        </td>
      </tr>
    </table>

    <table width='100%' height='500'>
        <tr>
            <td style="background:yellow"><child1 /></td>
            <td style="background:green"><child2 /></td>
        </tr>
        <tr>
            <td style="background:gray"><child3 /></td>
            <td style="background:cyan"><child4 /></td>
        </tr>
    </table>
  </div>
</template>

<script lang='ts'>
import Vue from 'vue';
import Component from 'vue-class-component';
import _ from 'lodash';
import child1 from '@/components/child-with-api1.vue';
import child2 from '@/components/child-with-api2.vue';
import child3 from '@/components/child-with-api3.vue';
import child4 from '@/components/child-with-api4.vue';

@Component({
  components:{
    child1,
    child2,
    child3,
    child4,
  },
  pageStore:{
    isPage:true,
    pageObject:{
      deep:true, //an option of watch
    },
  },
  watch: {
      pageCounter: function (newValue:any, oldValue:any) {
        if (newValue != oldValue)
          this.$sendPageData(newValue, 'pageCounter');
      },
      globalCounter: function (newValue:any, oldValue:any) {
        if (newValue != oldValue)
          this.$sendGlobalData(newValue, 'globalCounter');
      },
      globalObject: {
        deep:true,
        handler(newValue:any, oldValue:any) {
          console.log('globalObject handler :', newValue, oldValue);
          if (newValue != oldValue)
            this.$sendGlobalData(newValue, 'globalObject');
        }
      },
  },
})
export default class extends Vue {

  private pageObject: any = {
    strValue1:'string defaule',
    numberValue1:10,
    nestedObj :{
      nestedStrVal1:'nested string',
      nestedNumberVal1:101,
    }
  }

  private pageCounter = 100;

  private globalObject: any = {
      strValue1:'strValue1 defaule',
      strValue2:'strValue2 defaule',
      numberValue1:10,
      nestedObj :{
        nestedStrVal1:'nestedStrVal1 string',
        nestedNumberVal1:101,
      }
    };
  private globalCounter = 200;

  get title() {
      return this.$router.currentRoute.path;
  }

  created() {

    this.$setGlobalDataCallback((data:any) => {
      console.log('page2.vue : $setGlobalDataCallback', data);
      this.globalObject = data;
    }, 'globalObject');

    //Don't do this, it will end up causing an infinite feedback
    this.$setGlobalDataCallback((data:any) => {
      // console.log('page2.vue : $setGlobalDataCallback', data);
      this.globalCounter = data;
    }, 'globalCounter');

    this.$setPageDataCallback((data:any) => {
      // console.log('page2.vue : $setGlobalDataCallback', data);
      this.pageCounter = data;
    }, 'pageCounter');
  }

  updatePageObject() {
    this.pageObject = {
      strValue1:'strValue1 updated',
      strValue2:'strValue2 updated',
      numberValue1:20,
      nestedObj :{
        nestedStrVal1:'nestedStrVal1 string updated',
        nestedNumberVal1:201,
      }
    };
  }


}
</script>

<style>
td {
  text-align: left;
  width: 50%;
}
</style>