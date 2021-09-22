<template>
  <div class="desktop">
    <Folder @open="open" :type="'desktop'" :path="'/home'" />
  </div>

  <Window
    :ref="setWindowRef"
    v-for="currentWindow in windows"
    :key="currentWindow"
    @pointerdown="onWindowMouseDown"
    v-bind="currentWindow"
    :defaultX="mouseX"
    :defaultY="mouseY"
  >
    <Article
      v-if="currentWindow.type == 'article'"
      :path="currentWindow.path"
    />

    <Folder
      @open="open"
      v-if="currentWindow.type == 'folder'"
      :path="currentWindow.path"
    />

    <ImageElement
      v-if="currentWindow.type == 'image'"
      :path="currentWindow.path"
    />
    
    
  </Window>

</template>

<script>
import Article from "./components/Article.vue";
import Window from "./components/Window.vue";
// import Modal from './components/Modal.vue';
import Folder from "./components/Folder.vue";
import ImageElement from './components/ImageElement.vue'

export default {
  name: "App",

  components: {
    Window,
    Article,
    Folder,
    ImageElement
  },

  data() {
    return {
      windowRefs: [],
      search: window.location.search.replace("?", "").split("&"),
      mouseX: 0,
      mouseY: 0,
      windows: [],
    };
  },

  computed: {},

  methods: {
    onWindowMouseDown(event) {
      this.windowToTop(event.srcElement.closest(".modal"));
    },

    windowToTop(currentWindow) {
      let maxZIndex = 0;

      let modals = document.querySelectorAll(".modal");

      [].forEach.call(modals, (elem) => {
        let currentZIndex = window.getComputedStyle(elem).zIndex;
        if (parseInt(currentZIndex) > maxZIndex) {
          maxZIndex = parseInt(currentZIndex);
        }
      });

      currentWindow.style.zIndex = parseInt(maxZIndex) + 1;
    },

    open(event) {
      this.windows.push(event);
      this.$nextTick(() => {
        this.lastWindowOnTop();
      });
    },

    lastWindowOnTop() {
      let modals = document.querySelectorAll(".modal");
      this.windowToTop(modals[modals.length - 1]);
    },

    setWindowRef(ref) {
      this.windowRefs.push(ref);
    },
  },

  mounted() {
    document.addEventListener('pointermove', event => {
      this.mouseX = event.clientX - 50;
      this.mouseY = event.clientY - 20;
    })
  },
};
</script>

<style>

html {
  height: 100%;
}

body {
  background: var(--bg-color);
  /* background-image: url('./assets/back.jpeg'); */
  background-size:cover;
  background-repeat: no-repeat;
  margin: 0;
  height: 100% !important;
}

.desktop {
  padding: 20px
}

* {
  color: white;
}
</style>
