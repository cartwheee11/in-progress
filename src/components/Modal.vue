<template >
  <div ref="dom" @mouseup="mouseUp" @click.stop="click" class="container modal" :style="containerStyle">
      <slot />
  </div>
</template>

<script>
export default {
	props: {
		x: {
      required: false,
      default: 0,
      type: Number
    },

    y: {
      required: false,
      default: 0,
      type: Number
    },

    height: {
      required: false,
      default: window.innerHeight,
      type: Number
    },

    width: {
      required: false,
      default: window.innerWidth,
      type: Number
    },

    flexible: {
      required: false,
      default: false,
      type: Boolean,
    },
	},

  data() {
    return {
      currentX: this.x,
      currentY: this.y,
      currentHeight: this.height,
      currentWidth: this.width
    };
  },

  computed: {
    containerStyle: function () {
			return {
				top: this.currentY + 'px',
				left: this.currentX + 'px',
				height: this.currentHeight + 'px',
				width: this.currentWidth + 'px'
			}
		},
  },

  watch: {
    x: function() {
      this.currentX = this.x;
    },

    y: function() {
      this.currentY = this.y;
    }
  },

  mounted() {
    this.$emit('ref', this.$refs.dom)
  },

  methods: {
    mouseUp() { 
      this.currentHeight = window.getComputedStyle(this.$refs.dom).height
      this.currentWidth = window.getComputedStyle(this.$refs.dom).width
    }
  }
};
</script>

<style scoped>
  @keyframes show {
    from {
      transform: translate(0, +20px);
      opacity: 0;
    }

    to {
      transform: translate(0, 0);
      opacity: 1;
    }
  }

  ::-webkit-resizer {
    /* background: red; */
    /* display: block !important; */
    border-top: 1px solid white !important;
    border-left: 1px solid white !important;
    position: absolute;
    bottom: 2px;
    right: 2px;
  }

  .container {
    position: fixed;
    /* border: 1px var(--modal-border-color) solid; */
    /* box-shadow: 0 0 0px 1px var(--modal-border-color); */
    border-radius: 3px;
    background: var(--window-color);
    overflow: hidden;
    z-index: 0;
    min-width: 300px;
    min-height: 300px;
    resize: both;

    height: 100%;

    animation-name: show;
    animation-duration: 0.2s;
    animation-iteration-count: 1;
    /* padding-bottom: 20px; */
    /* padding-bottom: 20px; */
    
    /* transition: 0.01s; */
    /* -webkit-box-shadow: 0px 8px 35px 12px rgba(223, 223, 223, 0.32); */
    /* -moz-box-shadow: 0px 8px 35px 12px rgba(223, 223, 223, 0.32); */
    /* box-shadow: 0px 8px 35px 12px rgba(255, 255, 255, 0.15); */
  }
</style>