<template>
  <!-- <p>hello</p> -->
  <div class="container" :style=styles>
    <!-- <img :src="path" alt=""> -->
  </div>
</template>

<script>
export default {
  props: {
    path: {
      type: String,
      required: true
    }
  },

  data() {
    return {
      styles: {
        backgroundImage: `url(${this.path})`,
        backgroundSize: 'contain'
      }
    }
  },

  mounted() {
    console.log(this.path)
  }
}
</script>

<style scoped>
  .container {
    background-repeat: no-repeat;
    width: 100%;
    height: 100%;
    background-position: center;
  }
</style>