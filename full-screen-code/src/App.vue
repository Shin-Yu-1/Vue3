<template>
  <nav>
    <button @click="fullScreen = !fullScreen">Full Screen</button>
  </nav>
  <router-view @ScreenChange="ScreenChange" :fullScreen="fullScreen" />
</template>
<script>
import { ref } from '@vue/reactivity';
export default {
  setup () {
    const fullScreen = ref(false); // boolean button 기본값 false
    function ScreenChange (value) { // emit으로 받아서 value 변경
      fullScreen.value = value;
    };
    return { fullScreen, ScreenChange }
  }
}
</script>
