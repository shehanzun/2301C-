<template>
<div>
    <div id="yuan" v-show="checked=='true'" @click="fal">
      <img src="@/icon/yue.png" alt="">
  </div>

  <div id="yuan1" v-show="checked=='false'" @click="tru">
      <img src="@/icon/yue1.png" alt="">
  </div>
</div>
</template>
<script setup lang='ts'>
const checked=ref('true')
localStorage.setItem('state',JSON.stringify(checked.value))
import { ref } from "vue";

const fal=()=>{
    checked.value='false'
    localStorage.setItem('state',JSON.stringify(checked.value))
}

const tru=()=>{
    checked.value="true"
    localStorage.setItem('state',JSON.stringify(checked.value))
}
</script>
<style scoped lang='scss'>
#yuan{
    position: fixed;
    right: 30px;
    bottom: 150px;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #fff;
    box-shadow: 0px 0px 5px 2px #ccc;
    img{
      width: 20px;
      height: 20px;

    }
}

#yuan1{
    position: fixed;
    right: 30px;
    bottom: 150px;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #63a48e;
    box-shadow: 0px 0px 5px 2px #ccc;
    img{
      width: 20px;
      height: 20px;

    }
}
</style>