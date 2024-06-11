<script setup lang="ts">
import { onMounted, ref } from 'vue'
import gsap from 'gsap';
const duration = 2 // 缩短文字动画时长
const moveDuration = 2 // 移动动画时长
const x1 = ref(0)
const x2 = ref(100)
const x3 = ref(280)
const animation = ref('animation')
const echRef = ref<HTMLDivElement>()
const echWidth = ref(0)
const eRef = ref<HTMLDivElement>()
const eWidth = ref(0)
const xRef = ref<HTMLDivElement>()
const xWidth = ref(0)

const perRef = ref<HTMLDivElement>()
  const perWidth = ref(0)

const ndexRef = ref<HTMLDivElement>()
const ndexWidth = ref(0)
const click = ()=>{
  gsap.fromTo(echRef.value as HTMLDivElement, {
    width:echWidth.value,
  },{
    width: 0,
    duration
  })
  gsap.fromTo(eRef.value as HTMLDivElement, {
    width:eWidth.value,
  },{
    width: 0,
    duration:1
  })

  gsap.fromTo(perRef.value as HTMLDivElement, {
    width:perWidth.value,
  },{
    width: 0,
    duration
  })
  gsap.fromTo(ndexRef.value as HTMLDivElement, {
    width:ndexWidth.value,
  },{
    width: 0,
    duration
  })
  gsap.fromTo(xRef.value as HTMLDivElement, 
  { scaleX: 0.8, scaleY: 0.7 }, 
  { scaleX: 1, scaleY: 1, duration, })
  setTimeout(() => {
    gsap.to(x2,{
      value: 20,
      duration:moveDuration, 
      onUpdate:()=>{
        x2.value = x2.value
      }
    })
    gsap.to(x3,{
      value: 40,
      duration:moveDuration, 
      onUpdate:()=>{
        x3.value = x3.value
      }
    })
  }, duration*1000);
}

onMounted(() => {
    echWidth.value = echRef.value!.offsetWidth;
    eWidth.value = eRef.value!.offsetWidth;
    xWidth.value = xRef.value!.offsetWidth;
    perWidth.value = perRef.value!.offsetWidth;
    ndexWidth.value = ndexRef.value!.offsetWidth;

})
</script>

<template>
  <button @click="click">开始动画</button>
 <div class="container">
  <div :class="['card',animation]" :style="{'left': x1 + 'px'}">
    <div >T</div>
    <div ref="echRef" class="muti-word">ech</div>  
  </div>
  <div :class="['card',animation]" :style="{'left': x2 + 'px'}">
    <div ref="eRef" class="single-word">E</div> 
    <div ref="xRef" style="transform: scaleY(0.7) scaleX(0.8) ;transform-origin:  50% 80%; font-weight: 1000;">X</div>

    <div ref="perRef" class="muti-word">perience</div>
  </div>
 
  <div :class="['card',animation]" :style="{'left': x3 + 'px'}">
    <div>I</div>
    <div ref="ndexRef" class="muti-word">ndex</div>
  </div>
 </div>

  
</template>

<style scoped>
.zoomin{
  transform: scale(1.3);
}
.card{
  font-family: Arial;
font-size: 28px;
font-weight: 700;
line-height:1;
text-align: left;
display: flex;
position: absolute;

}
.single-word{
  overflow: hidden;
}
.muti-word{
  overflow: hidden;
}
.container{
  position: relative;
}



</style>
