/* eslint-disable @typescript-eslint/explicit-module-boundary-types */
<template>
  <div>
    <h2>Using decorations like @PageStore, @GlobalStore and so on</h2>
    <table width='100%' >
      <tr>
        <td>
          <p>
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
          <p>
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
            <b>myPageCounter : </b><input v-model="myPageCounter" type="number" /> 
          </p>
          <button @click="myPageCounter = Number(myPageCounter) + 10">myPageCounter + 10</button>
        </td>
        <td>
          <p>
            <b>myGlobalCounter : </b><input v-model="myGlobalCounter" type="number" /> 
          </p>
          <button @click="myGlobalCounter = Number(myGlobalCounter) + 10">myGlobalCounter + 10</button>
        </td>
      </tr>
    </table>

    <table width='100%' height='500'>
        <tr>
            <td style="background:yellow">
              <child1 />
            </td>
            <td style="background:green">
              <child2 />
            </td>
        </tr>
        <tr>
            <td style="background:gray">
              <child3 />
            </td>
            <td style="background:cyan">
              <child4 />
            </td>
        </tr>
    </table>
  </div>
</template>

<script lang='ts'>
import Vue from 'vue';
import Component from 'vue-class-component';
import _ from 'lodash';
import child1 from '@/components/child-with-decorators1.vue';
import child2 from '@/components/child-with-decorators2.vue';
import child3 from '@/components/child-with-decorators3.vue';
import child4 from '@/components/child-with-decorators4.vue';
import {
  AsPage,
  GlobalStore,
  PageStore,
  GlobalStoreBeforeReceive,
  GlobalStoreBeforeSend,
  PageStoreBeforeReceive,
  PageStoreReceived,
  PageStoreBeforeSend
} from 'vue-scoped-store';

@Component({
  components:{
    child1,
    child2,
    child3,
    child4,
  },
})
export default class extends Vue {
  @PageStore({deep:true})
  // eslint-disable-next-line @typescript-eslint/no-explicit-any
  private pageObject:any = null;
  @PageStore({path:"pageCounter"})
  private myPageCounter = 101;

  @AsPage()
  private isPage = true;

  @GlobalStore({deep:true})
  private globalObject = {
      strValue1:'strValue1 defaule',
      strValue2:'strValue2 defaule',
      numberValue1:10,
      nestedObj :{
        nestedStrVal1:'nestedStrVal1 string',
        nestedNumberVal1:101,
      }
    };

  @GlobalStore({path:"globalCounter"})
  private myGlobalCounter = 500;

  get title() : string {
      return this.$router.currentRoute.path;
  }

  created() : void {
    this.pageObject = {
      strValue1:'strValue1 defaule',
      strValue2:'strValue2 defaule',
      numberValue1:10,
      nestedObj :{
        nestedStrVal1:'nestedStrVal1 string',
        nestedNumberVal1:101,
      }
    };
  }

  @PageStoreBeforeSend('pageObject')
  onBeforeSendPageObject(val:any, oldVal:any, options:{proceed:boolean}) : void {
    console.log('onBeforeSendPageObject for pageObject in page4', val, oldVal, options);
  }

  @PageStoreBeforeReceive('pageObject')
  onBeforeReceivePageObject(val:any, oldVal:any, options:{proceed:boolean}) : void {
    console.log('onBeforeReceivePageObject  for pageObject in page4', val, oldVal, options);
  }

  @PageStoreBeforeReceive('myCounter')
  onBeforeReceiveMyCounter(val:any, oldVal:any, options:{proceed:boolean}) : void {
    console.log('onBeforeReceiveMyCounter for myCounter in page4', val, oldVal, options);
  }

  @PageStoreReceived('pageObject')
  onReceivedPageObject(val:any) : void {
    console.log('onReceivedPageObject for pageObject in page4', val);
  }

  @GlobalStoreBeforeSend('globalObject')
  onBeforeSendGlobalObject(val:any, oldVal:any, options:{proceed:boolean}) : void {
    console.log('onBeforeSendGlobalObject for globalObject in page4', val, oldVal, options);
  }

  @GlobalStoreBeforeReceive('globalObject')
  onBeforeReceiveGlobalObject(val:any, oldVal:any, options:{proceed:boolean}) : void {
    console.log('onBeforeReceiveGlobalObject for globalObject in page4', val, oldVal, options);
    //this will not be called at the moment
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

  updateByDeepCopy(path: string, value: any) : void {
    let clone = _.cloneDeep(this.pageObject);
    _.set(clone, path, value);
    this.pageObject = clone;
  }

}
</script>

<style>
td {
  text-align: left;
  width: 50%;
}
</style>