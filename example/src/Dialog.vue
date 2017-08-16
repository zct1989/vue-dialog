<template>
  <div class="dialog-wapper" v-show="visual">
    <div @click="handleClose('mask')" class="dialog-mask" v-if="modal" :style="{ zIndex: getMaskIndex() }"></div>
    <div class="dialog-body" :class="[`dialog-size-${size}`]" v-show="visual" :style="{zIndex:getBodyIndex(),top:top}">
      <div class="dialog-header">
        <slot name="title">
          <span class="dialog-header-title">{{title}}</span>
        </slot>
        <button type="button" class="dialog-header-btn" v-if="showClose" @click="handleClose">
          <svg version="1.1" id="图层_1" xmlns="http://www.w3.org/2000/svg"  x="0px" y="0px" viewBox="0 0 612 792" height="30px" width="30px">
          <g>
            <g>
              <defs>
                <rect id="SVGID_1_" x="44" y="134" width="523.92" height="524.88"/>
              </defs>
              <clipPath id="SVGID_2_">
                <use xlink:href="#SVGID_1_"  overflow="visible"/>
              </clipPath>
              <path clip-path="url(#SVGID_2_)" d="M339.453,396.411l220.539-220.539c4.684-4.688,7.028-10.832,7.028-16.973
                c0-6.14-2.344-12.281-7.028-16.969c-9.371-9.375-24.57-9.375-33.941,0L305.512,362.469L84.973,141.93
                c-9.375-9.375-24.571-9.375-33.942,0C46.344,146.614,44,152.759,44,158.899c0,6.141,2.344,12.285,7.031,16.969L271.57,396.411
                L51.031,616.95C46.344,621.634,44,627.778,44,633.919c0,6.144,2.344,12.285,7.031,16.972c4.684,4.684,10.828,7.028,16.969,7.028
                c6.141,0,12.285-2.344,16.969-7.028l220.543-220.539l220.539,220.539c4.683,4.684,10.828,7.028,16.969,7.028
                c6.144,0,12.285-2.344,16.972-7.028c4.684-4.687,7.028-10.828,7.028-16.972c0-6.141-2.344-12.282-7.028-16.969L339.453,396.411z
                M339.453,396.411"/>
            </g>
          </g>
          </svg>
          </button>
      </div>
      <slot>
      </slot>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'v-dialog',
    componentName: 'v-dialog',
    data() {
      return {
        maskIndex: 1000,
        bodyIndex: 1001
      }
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
      size: {
        type: String,
        default: 'small'
      },
      top: {
        type: String,
        default: '15%'
      },
      showClose: {
        type: Boolean,
        default: true
      },
      title: {
        type: String,
        default: '提示'
      }
    },
    methods: {
      handleClose(target) {
        if (target === 'mask' && !this.closeOnClickModal) {
          return
        } else {
          this.$emit('update:visual', false)
        }
      },
      getMaskIndex() {
        let parent = this.getParent()

        if (parent) {
          this.maskIndex = parent.maskIndex + 1000
        }

        return this.maskIndex
      },
      getBodyIndex() {
        let parent = this.getParent()

        if (parent) {
          this.bodyIndex = parent.bodyIndex + 1000
        }

        return this.bodyIndex
      },
      getParent() {
        var parent = this.$parent
        while (parent && parent.$options.componentName !== 'v-dialog') {
          parent = parent.$parent
        }
        return parent
      }
    }
  }
</script>

<style scoped>
  .dialog-wapper,
  .dialog-mask {
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    width: 100%;
    height: 100%;
  }

  .dialog-wapper * {
    text-align: left;
  }

  .dialog-body {
    position: fixed;
    top: 10%;
    height: 50%;
  }

  .dialog-mask {
    background-color: #000000;
    opacity: 0.3;
    z-index: 1000;
  }

  .dialog-body {
    background-color: #FFFFFF;
    z-index: 1001;
  }

  .dialog-size-tiny {
    width: 50%;
    left: 25%;
  }

  .dialog-size-small {
    width: 70%;
    left: 15%;
  }

  .dialog-size-large {
    width: 90%;
    left: 5%;
  }

  .dialog-size-full {
    width: 100%;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
  }

  .dialog-header {
    padding: 20px 20px 0
  }

  .dialog-header-title {
    line-height: 1;
    font-size: 16px;
    font-weight: 700;
    color: #1f2d3d;
  }

  .dialog-header-btn {
    float: right;
    background: transparent;
    border: none;
    outline: none;
    padding: 0;
    cursor: pointer;
  }

  svg {
    fill: rgb(191, 203, 217);
  }

  svg:hover {
    fill: rgb(32, 160, 255);
  }
</style>