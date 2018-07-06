/** 
 * @author: zhazhjie 
 * @email: zhazhjie@vip.qq.com
 * @date: 2018-06-16 11:51:37 
 * @version: 1.0 
 */

<template>
  <div class="select">
    <div class="more" :class='showFlag?"rotate180":""'></div>
    <input class="input" type="text" @click='showMore' @blur='hideMore' :value='showText' :readonly='isReadonly' ref='input'>
    <transition name='slide'>
      <div class="select-list" v-show='showFlag'>
        <ul>
          <li :class='showText==(item.text||item)?"active":""' v-for='(item,index) in list' :data-value='item.value||item' @mousedown='selectItem(item)' @touchstart='selectItem(item)'>{{item.text||item}}</li>
        </ul>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  props:{
    value:{
      
    },
    isDisable:{
      type:Boolean,
      default:false
    },
    isReadonly:{
      type:Boolean,
      default:true
    },
    list:{
      type:Array,
      required:true
    }
  },
  data() {
    return {
      showFlag:false,
      
    }
  },
  components: {

  },
  methods: {
    showMore(){
      this.showFlag=!this.showFlag;
    },
    hideMore(e){
      if(this.showFlag)
        setTimeout(()=>{
          this.showFlag=false
        },10)
    },
    selectItem(item){
      var val=item.value||item;
      var text=item.text||item;
      //console.log(item)
      //console.log(val)
      if(!val){
        return;
      }
      //this.showText=text;
      this.$emit('input',val);
      //this.showMore();
    }
  },
  computed: {
    showText(){
      var list=this.list;
      if(Object.prototype.toString.call(list[0])=='[object Object]'){
        var len=list.length;
        for(var i=0;i<len;i++){
          if(this.value==list[i].value){
            return list[i].text;
          }
        };
      }else{
        return this.value;
      }
    }
  },
  mounted(){
    
  }
}
</script>

<style scoped>
.select{
  position: relative;
  display: flex;
  border-radius: 5px;
  border: 1px solid #ccc;
  height: 40px;
  width: 200px;
}
.input{
  padding: 0 30px 0 10px; 
  width: 100%;
  height: 100%;
  cursor: pointer;
  position: relative;
  border: 0;
  outline: 0;
  background: none;
}
.more{
  /* font-family: 'iconfont'; */
  width: 30px;
  height: 100%;
  position: absolute;
  top: 0;
  right: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #999;
  cursor: pointer;
  transition: all 0.2s;
}
.more::before{
  content: '';
  position: absolute;
  width: 0;
  height: 0;
  border-top: 8px solid #ccc;
  border-left: 5px solid rgba(0, 0, 0, 0);
  border-right: 5px solid rgba(0, 0, 0, 0);
}
div.rotate180{
  transform: rotate(180deg);
  transition: all 0.2s;
}
.select-list{
  position: absolute;
  top: 120%;
  top: calc(100% + 10px);
  left: 0;
  width: 100%;
  border: 1px solid #ddd;
  padding: 5px 0;
  box-shadow: 0 2px 12px 0 rgba(0,0,0,.2);
  background: #fff;
  border-radius: 5px;
  z-index: 2;
  max-height: 5000px;
}
.select-list::after{
  content: '';
  width: 0;
  height: 0;
  position: absolute;
  top: -5px;
  left: 25px;
  border-bottom: 5px solid #fff;
  border-left: 5px solid rgba(0, 0, 0, 0);
  border-right: 5px solid rgba(0, 0, 0, 0);
}
.select-list::before{
  content: '';
  width: 0;
  height: 0;
  position: absolute;
  top: -6px;
  left: 25px;
  border-bottom: 5px solid #ccc;
  border-left: 5px solid rgba(0, 0, 0, 0);
  border-right: 5px solid rgba(0, 0, 0, 0);
}
.select-list li{
  list-style: none;
  height: 35px;
  line-height: 35px;
  padding-left: 10px;
  cursor: pointer;
}
.select-list li:hover{
  background: #F4F5FF;
}
.active{
  color: #4888ff;
}
.slide-enter-active,
.slide-leave-active{
  transition: all .3s;
}
.slide-enter,
.slide-leave-to{
  max-height: 0;
  opacity: 0;
  transform: translate3d(0, -10%, 0);
}
</style>