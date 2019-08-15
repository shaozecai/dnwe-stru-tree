<template>
    <div class="dnwe-stru-tree" v-click-outside="close">
      <div class="trigger" @click="toggle">
        <slot></slot>
        <input class="dnwe-tree-input" type="text" placeholder="请选择">
      </div>
      <div class="dnwe-stru-tree-box" v-if="isVisible">
        <div class="content">
          <CascaderItem :options="options" :getData="getData"></CascaderItem>
        </div>
      </div>
    </div>
</template>

<script>
import CascaderItem from './CascaderItem'
export default {
  mounted(){
   
  },
  components:{
    CascaderItem
  },
  name:'Cascader',
  props:{
    options:{
      type:Array
    },
    getData:{
      type:Function
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
.item
  padding 2px 0
.item span 
  user-select: none; 
.select-icon
  vertical-align: top;
  padding: 3px 4px 3px 0
  font-size 15px
  cursor pointer
.fa-check-square
    color #1185aa

.dnwe-stru-tree-box
  padding 5px 0 15px 0
  border 1px solid #999
  overflow hidden
  position absolute
  left 0
  top 30px
  width 100%
.dnwe-stru-tree-box .content
  max-height 280px
  overflow-y auto 
.get-icon
  font-size 18px;
  display inline-block
  width 16px
  line-height 1
  cursor pointer
.get-icon .fa-xs
  font-size 18px
.get-icon .fa-spinner
  font-size 13px
  animation: mymove 3s linear infinite;

.dnwe-stru-tree
  display inline-block
  position relative
.dnwe-tree-input
  padding 5px 10px
  font-size 14px
  outline none
  border 1px solid #999
  border-radius 3px
.content-stru
  padding-left 10px
  transition all .3s linear
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

@keyframes mymove
{
from {transform: rotate(0)}
to {transform: rotate(360deg)}
}

</style>
