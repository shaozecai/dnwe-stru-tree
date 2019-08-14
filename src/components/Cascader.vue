<template>
    <div class="dnwe-stru-tree" v-click-outside="close">
      <div class="trigger" @click="toggle">
        <slot></slot>
        <input class="dnwe-tree-input" type="text" placeholder="请选择">
      </div>
      <div class="dnwe-stru-tree-box" v-if="isVisible">
        <div class="content">
          <CascaderItem :options="options" @update="update"></CascaderItem>
        </div>
      </div>
    </div>
</template>

<script>
import CascaderItem from './CascaderItem'
export default {
  components:{
    CascaderItem
  },
  name:'Cascader',
  props:{
    options:{
      type:Array
    }
  },
  directives:{
    clickOutside:{
      inserted(el,bindings){ // 只在插入时绑定事件
        document.addEventListener('click',(e)=>{
          if(e.target === el || el.contains(e.target)){
              return;
          }
          bindings.value(); // 点击非自己、或者不是自己的儿子就关闭元素
        });
      }
    }
  },
  data(){
    return {isVisible:false}
  },
  methods:{
    update(value){
      console.log(this.options,value.id)
      let items = this.options.filter(item => item.id == value.id)[0];
      this.$emit('update',items)
    },
    close(){
        this.isVisible = false
    },
    toggle(){
      this.isVisible = !this.isVisible
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus">
.dnwe-stru-tree
  display inline-block
.dnwe-tree-input
  padding 5px 10px
  font-size 14px
  outline none
  border 1px solid #999
  border-radius 3px
.content-stru
  padding-left 10px
h3
  margin 40px 0 0

ul
  list-style-type none
  padding 0

li
  display inline-block
  margin 0 10px

a
  color #42b983
</style>
