<template>
  <div class="container">
    <div
      v-for="(elem, key) in content"
      :key="key"
    >
      <Icon @dblclick="iconClick(elem.title, key)"
        :img="elem.img"
        :title="elem.title"
      />
    </div>  
  </div>
  
</template>

<script>
let axios = require('axios');
import Icon from './Icon.vue'
export default {
  components: {
    Icon
  },

  props: {
    path: {
      type: String,
      default: 'home',
      required: false
    },
  },

  data() {
    return {
      content: []
    }
  },

  methods: {
    iconClick(title, key) {
      // console.log(title, key)
      let event = { 
        title, 
        type: this.content[key].type, 
        path: this.content[key].path
      }
      this.$emit('open', event)
      console.log(event)
    }
  },

  async mounted() {
    let folderContent = await axios(this.path);
    // console.log(await folderContent)

    await folderContent.data.forEach(elem => {
      let title = elem
      let extension = title.split('.')[1]

      let type = null
      if(extension == 'doc') {
        type = 'article'
      } else if(extension == 'app') {
        type = 'application'
      } else if(extension == undefined) {
        type = 'folder'
      }

      let img = null
      if(type == 'article') {
        img = 'img/document.png'
      } else if(type == 'application') {
        img = 'img/defaultWebApp.png'
      } else if(type == 'folder') {
        img = 'img/folder.png'
      }



      this.content.push({ 
        title, 
        img, 
        type, 
        path: this.path + '/' + title
      })
    })

    // console.log(await folderContent.data);
    // this.content = await folderContent.data.map(elem => ({ name: elem }))
  }

}
</script>

<style scoped>
  .container {
    display:  grid;
    grid-template-columns:  1fr 1fr 1fr 1fr;
    grid-gap:  20px;
  }

  div {
    /*border:  1px solid white;*/
    text-align: center;
  }
</style>