<template>
  <div id="app">
    <show-path
      v-show = "sectedPath.length"
      :path="sectedPath"
    >
    </show-path>
    <directory
      :name="tree.name"
      :type="tree.type"
      :contents="tree.contents"
      :parentPath="''"
      :filePath = "filePath"
      @isSelect="filePath"
      class="root-directory">
    </directory>
  </div>
</template>

<script>
import tree from "../public/static/node_modules.json"
import Directory from "./components/Directory/Directory.vue"
import ShowPath from "./components/ShowPath/ShowPath.vue"

export default {
  name: 'App',
  components: {
    Directory,
    ShowPath
  },
  data: () => ({
    tree,
    sectedPath: '',
    currentFileId: ''
  }),
  methods: {
    filePath (data) {
      this.sectedPath = data.path;
      this.currentFileId = data.id;
    },
    getCurrentFileId() {
      return this.currentFileId;
    }
  },
  provide: function () {
    return {
      getCurrentFileId: this.getCurrentFileId
    }
  }
}
</script>

<style>
#app {
  font-size: 18px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  max-width: 875px;
  margin: 75px auto 0;
  padding: 20px 15px;
}
.tree-node {
  display: block;
  border-left: 1px solid;
  padding: 15px 0 5px 15px;
  margin-left: 15px;
  cursor: pointer;
}
.root-directory {
  border-left: 0;
  margin-left: 0;
  padding: 0;
}
</style>