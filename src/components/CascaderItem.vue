<template>
    <div class="content-stru">
        <div v-for="(item,key) in options" :key="key">
            <div> 
                <i @click="getChildren(item)">&gt;</i> 
                <span @click="select(item)">口</span> 
                <span>{{item.name}}</span>
            </div>  
            <CascaderItem :options="item.children" @update="update"></CascaderItem>
        </div>
    </div>
</template>

<script>

export default {
  name:'CascaderItem',
  props:{
    options:{
      type:Array
    }
  },
  data(){
    return {}
  },
  mounted(){
      console.log(this.options)
  },
  methods:{
    getChildren(item){
        // 并通知父组件获取子节点 更新参数
        this.$emit('update',item)
    },
    select(item){
        // 获取当前节点下的组织架构 item.id  并通知父组件更新参数
     
    },
    update(value){
        console.log(this.options,value.id)
        // let items = this.options.filter(item => item.id == value.id)[0];
        // this.$emit('update',items)
    },
  }
};
</script>
