<template>
    <div class="content-stru">
        <div v-for="(item,key) in options" :key="key">
            <div class="item"> 
                <span class="get-icon" >
                  <font-awesome-icon v-if="item.children == null || item.children.length > 0" :icon="['fas', item.loading ? 'spinner': item.showChildren ? 'angle-down' : 'angle-right']" size="xs" @click="getChildren(item);"/>
                </span>
                <font-awesome-icon class="select-icon" :icon="['far', item.selected ? 'check-square' : 'square']" size="xs" @click="togglerSelect(item)"/>
                <span>{{item.name}}</span>
            </div>  
            <CascaderItem v-show="item.showChildren" :value="value" :options="item.children"  :getData="getData"></CascaderItem>
        </div>
    </div>
</template>

<script>

export default {
  computed:{
   
  },
  name:'CascaderItem',
  props:{
    options:{
      type:Array
    },
    getData:{
      type:Function
    },
    value:{
      type:Array,
      default:()=>{return []}
    }
  },
  data(){
    return {
     
    }
  },
  mounted(){
    
  },
  methods:{
    async getChildren(item){
      if(item.showChildren){
        item.showChildren = !item.showChildren
        return
      }
      if(item.children){
        item.showChildren = !item.showChildren
        return
      }

      let indx,showChildren
      this.options.forEach((element,index) => {
        if(element.id == item.id){
          indx = index;
          return
        }
      });
      this.$set(this.options[indx],'loading',true);
      let datas = await this.getData(item);
      this.$set(this.options[indx],'children',datas);
      this.$set(this.options[indx],'showChildren',!showChildren);
      delete(item.loading)
    },
    togglerSelect(item){      
      let indx,selected
      this.options.forEach((element,index) => {
        if(element.id == item.id){
          indx = index;
          selected = item.selected
          return
        }
      });
      this.$set(this.options[indx],'selected',!selected);
      if(this.options[indx].selected){
        this.$set(this.value,this.value.length,item);
      }else{
        this.value.forEach((element,index) => {
          if(element.id == item.id){
            this.value.splice(index,1);
            return false
          }
        });
      }
    },
  }
};
</script>
