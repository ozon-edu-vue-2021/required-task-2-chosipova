<template>
  <div class="tree-node" >
    <div
      :class="nodeClasses"
      :tabindex="1"
      :id="id"
      @click="isSelect"
      @keyup.enter="isSelect" 
    >
      <a
        v-if="type === 'link'"
        :href="target"
      >
        {{name}}
      </a>
      <span
        v-else
      >
        {{name}}
      </span>
    </div>
  </div>
</template>

<script>

const uniqueId = require('lodash.uniqueid');

export default {
  name: 'File',
  props: {
    type: {
      type: String,
      default: 'file'
    },
    name: {
      type: String,
      default: 'name'
    },
    target: {
      type: String,
      default: 'target'
    },
    parentPath: {
      type: String,
      default: ''
    }
  },
  computed: {
    nodeClasses() {
      return [{
        'selected': this.selected,
        'link': this.type === 'link',
        'file': this.type === 'file',
      }]
    },
    id() {
      return uniqueId('id')
    },
    selected() {
      return this.id === this.getCurrentFileId()
    },
    path() {
      return this.parentPath + "/" + this.name
    }
  },
  inject: ['getCurrentFileId'],
  methods: {
    isSelect() {
      this.$emit('isSelect', {
        path: this.path,
        id: this.id
      });
    }
  }
}
</script>

<style scoped>
.tree-node {
  padding-top: 15px;
  padding-bottom: 0;
  cursor: default;
}
.link,
.file {
  padding: 10px 15px;
  cursor: pointer;
  border-radius: 6px;
  display: block;
  border: 2px solid #fff;
}
.link a {
  color: #2c3e50;
  text-decoration: underline;
}
.file.selected {
  background: #1B4965;
  border: 2px solid #1B4965;
  color: #fff;
}
.link.selected {
  background: #F18F01;
  border: 2px solid #F18F01;
  color: #fff;
} 
.link.selected a {
  color: #fff;
}
.file:focus,
.file:focus-visible,
.link:focus,
.link:focus-visible {
  border: 2px solid #CE2D4F;
  outline: 0;
}
.file.selected:focus,
.file.selected:focus-visible {
  border: 2px solid #1B4965;;
}
.link.selected:focus,
.link.selected:focus-visible {
  border: 2px solid #F18F01;
} 
</style>