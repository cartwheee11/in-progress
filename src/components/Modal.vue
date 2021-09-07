<template @click="click">
  <div ref="dom" @click="click" class="container modal" :style="containerStyle">
    
      <slot />

  </div>
</template>

<script>
export default {
  data() {
    return {
      
    };
  },

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
	},

  computed: {
    containerStyle: function () {
			return {
				top: this.y + 'px',
				left: this.x + 'px',
				height: this.height + 'px',
				width: this.width + 'px'
			}
		},
  },

  mounted() {
    this.$emit('ref', this.$refs.dom)
  },

  methods: {
    click() {

    }
  }
};
</script>

<style scoped>
  .container {
    position: fixed;
    border: 1px white solid;
    border-radius: 10px;
    background: black;;
    overflow:  hidden;
    z-index: 0;
  }
</style>