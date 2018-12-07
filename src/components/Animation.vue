<template>
  <div class="animation">
    <div class="content1" :ref="aniamtionRef1"></div>

    <div class="content2" :ref="aniamtionRef2" v-if="animationConfig2"></div>
    <slot  class="title"></slot>
  </div>
</template>

<script>
import lottie from 'lottie-web'

export default {
  name: 'App',
  data () {
    return {
      cover1: '',
      cover2: '',
    }
  },
  props: {
      aniamtionRef1: {
          type: String,
          default: ''
      },
      aniamtionRef2: {
          type: String,
          default: ''
      },
      animationConfig1: {
          type: Object,
          default: function () {
              return {
                  renderer: 'svg',
                  loop: false,
                  autoplay: true,
                  path: ''
              }
          }
      },
      animationConfig2: {
          type: Object,
          default: function () {
              return {}
          }
      }
  },
  components: {},
  mounted () {
    let vm = this
    let element1 = vm.$refs[vm.aniamtionRef1]
    let config1 = {}

    config1 = { 'container': element1, ...vm.animationConfig1 }
    vm.cover1 = lottie.loadAnimation(config1);

    if (vm.animationConfig2) {
        let element2 = vm.$refs[vm.aniamtionRef2]
        let config2 = {}
        config2 = { 'container': element2, ...vm.animationConfig2 }
        vm.cover2 = lottie.loadAnimation(config2);
    }
  }
}
</script>

<style lang="scss" scoped>
.animation {
    width: 100%;
    height: 100vh;
    position: relative;
    .content1 {
        position: absolute;
        top: 0;
        left: 0;
        z-index: 1;
    }
    .content2 {
        position: absolute;
        top: 0;
        left: 0;
        z-index: 10;
    }
    .title {
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        position: absolute;
        top: 0;
        left: 0;
        z-index: 20;
        color: white;
    }
}
</style>
