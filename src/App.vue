<template>
  <button @click="clickHandler">Click me :)</button>
  <Article 
    v-for="(id) in openedArticles"
    :key="id"
    @click="windowClick(id)"
    :path="openedWindows[id].path"
    :defaultX="openedWindows[id].defaultX"
  />

  <windows-manager/>



</template>

<script>

import Article from "./components/Article.vue";
import WindowsManager from "./components/WindowsManager.vue";
// import Modal from "./components/Modal.vue
import Vue from 'vue'
export default {
  name: "App",

  components: {
    // Window,
    Article,
    WindowsManager
  },

  data() {
    return {
      search: window.location.search.replace("?", "").split("&"),
      mouseX: 0,
      mouseY: 0,
      openedModals: [
        {
          content: 'Hello, World!',
          x: 100,
          y: 100,
          width: 200,
          height: 200
        }
      ],
      openedWindows: [
        // {
        //   type: 'article',
        //   path: 'home/articles/second.html',
        //   defaultX: 100
        // },

        // {
        //   type: 'article',
        //   path: 'home/articles/first.html'
        // },
      ],


    };
  },

  computed: {
    openedArticles() {
      let res = [];
      this.openedWindows.forEach((elem, id) => {
        if(elem.type === 'article') {
          res.push(id);
        }
      })

      console.log(res)
      return res;
    },
  },

  methods: {
    clickHandler() {
      var ComponentClass = Vue.extend(Window);
      var instance = new ComponentClass();
      console.log(instance)
    },

    


    windowClick(id) {
      // this.openedWindows.push(elem)
      let elem = this.openedWindows[id];
      console.log(id);
      console.log(elem)
      // // console.log(this.openedWindows)
      // this.openedWindows.push(elem)
      // delete this.openedWindows[1]
      // console.log(id)
      // // this.openedWindows.splice(id - 1, 1)
      this.openedWindows = this.openedWindows.filter((elem, id) => id != 0);
      // console.log(this.openedWindows)


      
      // console.log(elem)
      // this.openedWindows = this.openedWindows.filter(el => JSON.stringify(el) != JSON.stringify(elem));
      // console.log(this.openedWindows)
      // // console.log(this.openedWindows)


    }
  }
  ,

  mounted() {

    document.onmousemove = (event) => {
      this.mouseX = event.pageX;
      this.mouseY = event.pageY;
    }
  }
};
</script>

<style>
body {
  background: black;
  margin: 0;
}

* {
  color: white;
}
</style>
