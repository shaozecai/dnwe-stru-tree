<template>
    <div>
      <Cascader :options="options" v-model="value" @update="update">cesss</Cascader>
      <br>
      <br>
      <br>
    </div>
</template>

<script>
import Cascader from './components/Cascader';
import data from './data'
export default {
    methods:{
      update(value){
        console.log('update',value)
        this.$set(this.options[0],'children',[{id:'12',name:'test11'},{id:'13',name:'test22'}])
      }
    },
    data(){
      return {
        options: data,
        value:['001']
      }
    },
    components:{
        Cascader
    }
}
</script>