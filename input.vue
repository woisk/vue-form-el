/** 
 * @author: zhazhjie 
 * @email: zhazhjie@vip.qq.com
 * @date: 2018-06-12 16:26:43 
 * @version: 1.0 
 */

<template>
  <label class="input">
    <span class="for-text" ref='forText'><slot/></span>
    <input :type="type" class="text" :value='value' @input='change' :disabled='isDisable' @focus='focus' @blur='blur'>
    <span class="line" ref='line'></span>
  </label>
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
    type:{
      type:String,
      default:'text'
    },
  },
  data() {
    return {

    }
  },
  components: {

  },
  methods: {
    change(e){
      this.$emit('input',e.target.value)
      //console.log(e.target.value)
    },
    focus(){
      this.$refs.forText.className='for-text to-top'
      this.$refs.line.className='line hide'
    },
    blur(e){
    	if(e.target.value)
	      return;
	    this.$refs.forText.className='for-text'
	    this.$refs.line.className='line'
    }
  },
  computed: {

  },
  mounted(){
    //console.log(this.value)
  }
}
</script>

<style scoped>
.input{
	width: 300px;
    height: 45px;
    display: flex;
    flex-direction: column;
    padding: 0 10px;
    position: relative;
    border-bottom: 1px solid #ddd;
    text-align: left;
  }
  .for-text{
    height: 16px;
    line-height: 16px;
    position: relative;
    top: 50%;
    margin-top: -8px;
    color: #999;
    transition: all 0.2s linear;
  }
  .text{
    width: 100%;
    height: 29px;
    border: 0;
    outline: 0;
    background: none;
    position: relative;
    z-index: 1;
  }
  .line{
    position: absolute;
    width: 100%;
    height: 2px;
    background: #5b88ed;
    bottom: -1px;
    left: 0;
    transform: scale(0, 1);
    transition: all 0.2s linear;
  }
  .to-top{
    top: 0;
    margin-top: 0;
    font-size: 14px;
    color: #5b88ed;
    transition: all 0.2s linear;
  }
  .hide{
    transform: scale(1, 1);
    transition: all 0.2s linear;
  }
</style>
