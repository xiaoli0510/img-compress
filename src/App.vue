<script setup>
import { ref } from 'vue'
import dog from './assets/dog.jpg'
const url = ref(dog)
const resUrl = ref('')
const compress = (imgW,imgH,ratio) => {
  const img = new Image()
  img.src = url.value
  img.crossOrigin = 'Anonymous'; 
  img.onload = () => {
    const canvas = document.createElement('canvas');
    canvas.width = imgW
    canvas.height = imgH
    const ctx = canvas.getContext('2d');
    ctx.drawImage(img,0,0,imgW,imgH)
    const base64 = canvas.toDataURL('image/jpeg', ratio) 
    resUrl.value = base64
  }
}
</script>

<template>
  <img :src="url" />
  <br/>
  <button @click="compress(200,200,.5)">点击压缩</button>
  <br/>
  <img :src="resUrl"/>

</template>