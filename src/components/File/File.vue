<template>
  <div class="tree-node">
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

export default {
  name: 'File',
  data: () => ({
    selected: false,
    selectedPath: ''
  }),
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
    path() {
      return this.parentPath + "/" + this.name
    }
  },
  methods: {
    isSelect() {
      this.selected = !this.selected;
      let newPath = '';
      (this.selected) ? newPath = this.path : newPath = this.parentPath
      this.$emit('isSelect', {
        path: newPath
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