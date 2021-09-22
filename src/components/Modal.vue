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

  .container {
    position: fixed;
    border: 3px #fff solid;
    border-radius: 22px;
    /* background: #000; */
    background: var(--window-color);
    overflow:  hidden;
    z-index: 0;
    min-width: 300px;
    min-height: 300px;
    resize: both;

    animation-name: show;
    animation-duration: 0.2s;
    animation-iteration-count: 1;
    /* transition: 0.01s; */

    /* -webkit-box-shadow: 0px 8px 35px 12px rgba(223, 223, 223, 0.32); */
    /* -moz-box-shadow: 0px 8px 35px 12px rgba(223, 223, 223, 0.32); */
    /* box-shadow: 0px 8px 35px 12px rgba(255, 255, 255, 0.15); */
  }
</style>