<template>
  <modal @ref="onRef" v-if="isOpened" :x=x :y=y :height=height :width=width >
    <div class="container">

      <div @mousedown="onMouseDown" class="top-bar">
        <div class="title-container">
          <div class="title">
            <p>{{title}}</p>
          </div>
        </div>

        <div class="controls" ref="controlsDOM">
          <button>minimize</button> <button @click="closeWindow">close</button> 
        </div>

        <div class="clear"></div>
      </div>

      <div class="content-container">
        <div class="content">
          <slot/>
        </div>
      </div>

      <div class="bottom-bar"></div>
    </div>
  </modal>
</template>

<script>
import Modal from "./Modal.vue";


export default {
  components: {
    Modal,
  },

  name: "Window",

  props: {
    defaultX: {
      type: Number,
      required: false,
      default: 0
    }, 

    defaultY: {
      type: Number,
      required: false,
      default: 0
    },

    defaultHeight: {
      type: Number,
      required: false,
      default: 400
    },

    defaultWidth: {
      type: Number,
      required: false,
      default: 600
    },

    title: {
      type: String,
      required: false,
      default: 'default title'
    }
  },

  data() {
    return {
      isOpened: true,
      titleStyles: '0px',
      x: this.defaultX,
      y: this.defaultY,
      height: this.defaultHeight,
      width: this.defaultWidth,
      isMouseDown: false,
      whereClickWas: {
        x: null,
        y: null
      }
    }
  },

  mounted() {
    document.addEventListener('mousemove', event => {
      if(this.isMouseDown) {
        this.x = event.clientX - this.whereClickWas.x;
        this.y = event.clientY - this.whereClickWas.y; 
      }
    })

    document.addEventListener('mouseup', () => {
      this.isMouseDown = false
    })
  },

  methods: {
    closeWindow() {
      this.isOpened = false;
    },

    onRef(){
      // this.$emit("ref", ref);
    },

    onMouseDown(event) {
      this.whereClickWas = {
        x: event.clientX - this.x,
        y: event.clientY - this.y
      }

      this.isMouseDown = true;
    }
  },

  watch: {
    isMounted() {
      this.titleStyles = {
        
        width: (this.width - parseInt(getComputedStyle(this.$refs.controlsDOM).width) - 10) + 'px'
      }
    }
  },
};
</script>

<style scoped>
  .top-bar {
    border-bottom: 0.5px solid #333;
    width: 100%;
    position: absolute;
    background: black;
  }

  .controls {
    /* float: right; */
    position: absolute;
    right: 0px;
    padding: 5px 20px;
  }

  .title-container {
    display: block;
    float: left;
    padding: 5px 20px;
  }

  .title {
    padding: 5px 10px
  }

  .title p{
    padding: 0;
    margin: 0
  }
  
  .container {
    height: 100%;
    width: 100%;
    display:  block;
  }

  .content-container {
    padding: 20px;
    padding-top: 100px;
    overflow-y: scroll;
    height: 100%;
  }

  .content {
    /*padding-bottom:  20px;*/
  }
    

  .content-container::-webkit-scrollbar {
    width: 0;
  }

  .clear {
    clear: both;
  }
</style>