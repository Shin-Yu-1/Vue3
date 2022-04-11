<template>
  <div class="home">
    <div  class="txt"><h2>Full Screen</h2></div>
    <div id="img"><img alt="Vue logo" src="../assets/logo.png"></div>
  </div>
</template>

<script>
import { watch } from '@vue/runtime-core';
export default {
  props: {
    fullScreen: { type: Boolean }
  },
  setup (props, { emit }) {
    watch(() => props.fullScreen, (newVal) => { // 변경값 감시
    // 지정된 id값만 가지고 전체화면 하기
      const img = document.getElementById('img');
      if (newVal === true) { // true -> 전체화면
          if (img.requestFullscreen) return img.requestFullscreen();
          if (img.webkitRequestFullscreen) return img.webkitRequestFullscreen();
          if (img.mozRequestFullScreen) return img.mozRequestFullScreen();
          if (img.msRequestFullscreen) return img.msRequestFullscreen();
      } else { // 전체화면 종료 시 emit으로 true 전달하여 다시 전체화면 가능하도록 작성함.
          if (document.exitFullscreen) { emit('fullScreenTrue', true); return document.exitFullscreen(); };
          if (document.webkitCancelFullscreen) { emit('fullScreenTrue', true); return document.webkitCancelFullscreen(); };
          if (document.mozCancelFullScreen) { emit('fullScreenTrue', true); return document.mozCancelFullScreen(); };
          if (document.msExitFullscreen) { emit('fullScreenTrue', true); return document.msExitFullscreen(); };
      }
    });
  }
}
</script>