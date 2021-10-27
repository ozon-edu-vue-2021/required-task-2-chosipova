<template>
  <div 
    class="tree-node"
    >
    <directory-title
      :name = "name"
      @click="toggle"
    />
    <tree-children 
      v-if="opened"
      :children="contents"
    />
  </div>
</template>

<script>

  export default {
    name: 'Directory',
    beforeCreate: function () {
      this.$options.components.TreeChildren = require("../TreeChildren/TreeChildren.vue").default;
      this.$options.components.DirectoryTitle = require(".//DirectoryTitle.vue").default;
    },
    data: () => ({
        opened: false
    }),
    props: {
      name: {
        type: String,
        default: 'name'
      },
      type: {
        type: String,
        default: 'directory'
      },
      contents: {
        type: Array,
        default: () => ([])
      }
    },
    methods: {
      toggle() {
        this.opened = !this.opened;
      }
    }
  }
</script>
