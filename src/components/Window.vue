<template>
  <modal @ref="onRef" v-if="isOpened" :x=x :y=y :height=height :width=width >
    <div class="container window-container">

      <div @pointerdown="onMouseDown" class="top-bar">
        <div class="title-container">
          <div class="title">
            <p>{{title}}</p>
          </div>
        </div>

        <div class="controls" ref="controlsDOM">
          <!-- <button>_ Minimize</button>  -->
          <button @click="closeWindow">X Close</button> 
        </div>

        <div class="clear"></div>
      </div>

      <div class="content-container">
        <div class="content">
          <slot/>
        </div>
      </div>
      <!-- <div class="bottom-bar"></div> -->
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
    document.addEventListener('pointermove', event => {
      if(this.isMouseDown) {
        this.x = event.clientX - this.whereClickWas.x;
        this.y = event.clientY - this.whereClickWas.y; 
      }
    })

    document.addEventListener('pointerup', () => {
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
    /* border: 5px solid var(--bg-color); */
    right: 5px;
    top: 5px;
    left: 5px;
    background: var(--window-top-bar-color);
  }

  .controls {
    position: absolute;
    /* float: right; */
    right: 5px;
    top: -3px;
    right: 0px;
    /* padding: 0px 20px; */
    padding-right: 5px;
  }

  .controls button {
    background: rgb(255, 59, 59);
    color: white;
    height: 26px;
    margin-top: 0px;
    z-index: 10;
    border-radius: 0px;
    /* position: absolute; */
    margin-bottom: 5px;
    /* width: 26px; */
  }

  .controls button:hover{
    background: rgb(214, 53, 53);
  }

  .controls button:active{
    background: rgb(176, 51, 51);
  }


  .title-container {
    display: block;
    float: left;
    padding: 0px 0px;
  }

  .title {
    padding: 5px 10px;
    color: black;
    text-decoration: underline;
  }

  .title p{
    padding: 0;
    margin: 0;
    text-transform: uppercase;
    color: black;
  }

  .window-container {
    border: solid white 1px;
  }
  
  .container {
    height: 100%;
    display: flex;
    flex-direction: column; 
  }

  

  /* .modal {
    border: solid white 1px;
  } */

  .content-container {
    overflow-y: scroll;
    z-index: 0;
    height: 100%;
  }

  .content {
    /* padding-bottom:  20px; */
    /* width: 100%; */
    height: 100%;
  }
    

  .content-container::-webkit-scrollbar {
    width: 0;
  }

  .clear {
    clear: both;
  }
</style>