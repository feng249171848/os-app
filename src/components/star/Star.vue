<template>
  <div class="star">
    <span v-for="(itemClass,index) in itemClasses" class="star-item" :class="itemClass" :key="index"></span>    
  </div>
</template>

<script>
// 星星的长度
const LENGTH = 5
const CLS_ON = 'on'
const CLS_HALF = 'half'
const CLS_off = 'off'
export default {
  name: 'Star',
  props:{
    score:{
      type:Number
    }
  },
  computed:{
    itemClasses(){
      let result = []; // 存储星星
      // 4.7
      let score = Math.floor(this.score*2) / 2;
      // 半星
      let hasDecimal = score%1 !== 0; //整数为0，false
      // 全星
      let integer = Math.floor(score);
      // 遍历全星
      for (let i = 0; i < integer; i++){
        result.push(CLS_ON)
      }
      // 处理半星
      if(hasDecimal){
        result.push(CLS_HALF);
      }
      // 补齐
      while(result.length < LENGTH){
        result.push(CLS_off);
      }
      
      return result
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.star{
		font-size: 0;
	}
	.star .star-item{
		display: inline-block;
		width: 10px;
		height: 10px;
		margin-right: 3px;
		background-repeat: no-repeat;
		background-size: 10px 10px;
	}
	.star .star-item:last-child{
		margin-right: 0;
	}
	
	/* 三种图片类型*/
	.star .on{
		background-image: url(img/star24_on@2x.png);
	}
	.star .half{
		background-image: url(img/star24_half@2x.png);
	}
	.star .off{
		background-image: url(img/star24_off@2x.png);
	}
</style>
