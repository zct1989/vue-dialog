<template>
  <div class="dialog-wapper" v-show="visual">
    <div @click="clickMask" class="mask" v-if="modal"></div>
    <div class="dialog-body" v-show="visual">
      <slot>
      </slot>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'v-dialog',
    data() {
      return {}
    },
    props: {
      visual: {
        type: Boolean,
        default: false
      },
      modal: {
        type: Boolean,
        default: true
      },
      closeOnClickModal: {
        type: Boolean,
        default: true
      },
      size:{
        type: String,
        default: 'small'
      }
    },
    methods:{
      clickMask(){
        if(this.closeOnClickModal){
          this.$emit('update:visual', false)
        }
      }
    }
  }
</script>

<style>
  .dialog-wapper,
  .mask {
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    width: 100%;
    height: 100%;
  }

  .dialog-body {
    position: fixed;
    width: 80%;
    height: 80%;
    left: 10%;
    top: 10%;
  }

  .mask {
    background-color: #000000;
    opacity: 0.3;
    z-index: 1000;
  }

  .dialog-body {
    background-color: #FFFFFF;
    z-index: 1001;
  }
</style>