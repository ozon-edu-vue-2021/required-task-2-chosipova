<template>
  <div class="tree-node" :id="id">
    <div
      :class="nodeClasses"
      @click="isSelect"
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
  transition: 0.2s;
}
.link a {
  color: #2c3e50;
  text-decoration: underline;
}
.file.selected {
  background: #1B4965;
  color: #fff;
}
.link.selected {
  background: #F18F01;
  color: #fff;
} 
.link.selected a {
  color: #fff;
}
</style>