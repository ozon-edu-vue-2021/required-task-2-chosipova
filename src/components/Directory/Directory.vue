<template>
  <div 
    class="tree-node" 
    >
    <directory-title
      :tabindex="1"
      :name = "name"  
      @click="toggle"
      @keyup.enter="toggle"
    />
    <tree-children
      ref="dir"
      v-if="opened"
      :children="contents"
      :parentPath="path"
      :filePath="filePath"
    />
  </div>
</template>

<script>
  export default {
    name: 'Directory',
    components: {
      TreeChildren: () => import('../TreeChildren/TreeChildren.vue'),
      DirectoryTitle: () => import('./DirectoryTitle.vue')
    },
    data: () => ({
      opened: false,
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
      },
      parentPath: {
        type: String,
        default: ''
      },
      filePath: {
        type: Function,
        required: true
      }
    },
    computed: {
      path() {
        return this.parentPath + "/" + this.name
      }
    },
    methods: {
      toggle() {
        this.opened = !this.opened;
        let newPath = '';
        (this.opened) ? newPath = this.path : newPath = this.parentPath
        this.$emit('isSelect', {
          path: newPath
        });
      }
    }
  }
</script>
