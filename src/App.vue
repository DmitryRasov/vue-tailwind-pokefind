<template>
  <div class="p-14">
    <router-link :style="{ color: colorCache }" class="flex justify-center text-4xl" to="/">Pokemon finder</router-link>
  </div>
  <router-view />
</template>


<style>
body{
  background: #ddc3ff;
}
</style>
<script>
import {ref} from 'vue'
export default {
  setup(){
    const colorCache = ref('')
    function randomColor() { colorCache.value  =  "#" + Math.floor(Math.random() * 16777215).toString(16) }
    randomColor()

  return {
      randomColor, colorCache
    }
  }
}

</script>
<style>
::-webkit-scrollbar { display: none }
</style>