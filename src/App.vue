<template>
    <div>
      <Cascader :options="options" v-model="value" :getData="getData"></Cascader>
    </div>
</template>

<script>
import Cascader from './components/Cascader';
import data from './data'
import { Promise } from 'q';
export default {
    methods:{
      async getData(item){
        return new Promise((resolve,reject)=>{
          setTimeout(() => {
             let result = data.filter(t=>t.pid === item.id);
             resolve(result); // 将获取到的数据传递出去
          }, 1000);
        })
      }
    },
    data(){
      return {
        options: data.filter(item=>item.pid == 0),
        value:[
          // { "id": '1',"name": "上海", pid: '0', isLeaf:'0'}
          ]
      }
    },
    components:{
        Cascader
    },
    computed:{
      
    }
}
</script>