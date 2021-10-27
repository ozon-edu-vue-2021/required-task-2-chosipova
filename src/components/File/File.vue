<template>
  <div 
    class="tree-node"
    >
    <a
      v-if="type === 'link'"
      :href="target"
      class="link"
      @click="selected($event.target)"
    >
      {{name}}
    </a>
    <span
      v-else
      class="file"
      @click="selected($event.target)"
    >
      {{name}}
    </span>
  </div>
</template>

<script>

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
    }
  },
  methods: {
    selected: function(elem) {
      let range = document.createRange();
      range.selectNode(elem);
      window.getSelection().removeAllRanges();
      window.getSelection().addRange(range);
    }
  }
}
</script>

<style scoped>
.tree-node {
  cursor: default;
}
.link,
.file {
  margin-left: 15px;
  cursor: pointer;
}
.link {
  color: #2c3e50;
  text-decoration: underline;
}
</style>