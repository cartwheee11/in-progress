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
          <!-- <button>Minimize</button>  -->
          <button @click="closeWindow">x</button> 
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
    border: 5px solid var(--bg-color);
    right: 5px;
    top: 5px;
    left: 5px;
    /* border-radius: 4px; */
    /* width: 100%; */
    /* position: absolute; */
    /* background: var(--window-color); */
    /* box-shadow: 4px 4px 8px 10px rgba(34, 60, 80, 0.2) !important; */
    background: black;
    
    /* border-radius: 20px; */

    /* top: 5px; */
    /* right: 5px; */
    /* background: rgb(2,0,36); */
    /* background: linear-gradient(90deg, rgba(2,0,36,1) 0%, rgba(9,9,121,1) 35%, rgba(9,9,121,1) 35%, rgba(0,212,255,1) 100%); */
  }

  /* .top-bar:after {
    content: " ";
    position: absolute;
    z-index: -1;
    top: 5px;
    left: 5px;
    right: 5px;
    bottom: 5px;
    border: 5px solid #ffea00;
  } */

  .controls {
    /* position: absolute; */
    float: right;
    right: 0px;
    /* padding: 0px 20px; */
    padding-right: 5px;
  }

  .controls button {
    background: rgb(255, 255, 255);
    /* color: white; */
    height: 26px;
    width: 26px;
  }

  .title-container {
    display: block;
    float: left;
    padding: 0px 20px;
  }

  .title {
    padding: 5px 10px;
    text-decoration: underline;
  }

  .title p{
    padding: 0;
    margin: 0;
    text-transform: uppercase;
    /* color: black; */
  }
  
  .container {
    height: 100%;
    width: 100%;
    display:  block;
  }

  .content-container {
    padding: 20px;
    padding-top: 50px;
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